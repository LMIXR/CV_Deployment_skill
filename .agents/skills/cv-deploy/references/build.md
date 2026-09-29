# 依赖编译

来源：`qt/`、`python/`、`paddle/ubuntu.md`、`tkdnn/ubuntu.md`、`ubuntu/cuda.md`；见[来源索引](source-index.md)。FFmpeg / GStreamer 的细节在[视频接入](video.md)。

## 构建关系与库发现

先识别项目使用的 CMake、qmake、Autotools、MSBuild 或 nmake。复用它的构建方式与工具版本。Linux / macOS 不要用全局编译器软链接替换实现项目降级；通过项目构建参数指定编译器。

路径分为源码目录、构建目录、安装前缀。指定 `CMAKE_PREFIX_PATH`、项目的 `*_DIR`、`PKG_CONFIG_PATH` 或显式 include / lib 路径，避免把所有依赖拷进系统目录。

通用 CMake 命令形状如下，变量由目标项目提供；多配置生成器需给 build / install 增加实际 `--config`：

```sh
cmake -S "$SOURCE_DIR" -B "$BUILD_DIR" \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX="$INSTALL_PREFIX"
cmake --build "$BUILD_DIR" --parallel "$BUILD_JOBS"
cmake --install "$BUILD_DIR"
```

`BUILD_JOBS` 按可用内存决定；原文的 `-j8` / `-j16` 不是固定要求。配置或编译无须 root，写受保护安装目录时才处理对应权限。

## OpenCV

原文分别记录 3.4 和 4.2，其中 4.2 涉及 contrib、CUDA、GStreamer 及构建时下载资源。

处理顺序：

1. 对齐 `opencv` 与 `opencv_contrib` 的版本；确定应用所需模块及 C++ / Python 接口。
2. 配置安装前缀、`OPENCV_EXTRA_MODULES_PATH`；根据消费方决定是否生成 pkg-config 文件。
3. 按需求启用 CUDA、DNN CUDA、GStreamer 或 FFmpeg；从该版本构建配置确认准确选项，不批量沿用旧开关。
4. CUDA 架构取目标 GPU 能力及所选 Toolkit 支持范围。原文“删除 5.3 以下”的经验只属于当时环境。
5. 遇到配置期下载失败，查看下载日志中资源名、版本与摘要，准备对应缓存。原文举例 `boostdesc_bgm.i`、IPPICV、`face_landmark_model.dat`，它们是额外构建资源，不应误判为编译器故障。

典型问题：

| 现象 | 优先定位 |
| --- | --- |
| `nvcuvid.h` / `nvOpticalFlowCommon.h` 缺失 | 项目是否启用了相应模块、SDK 版本和 include 路径 |
| `dynlink_nvcuvid.h` 缺失 | 旧 OpenCV 与 Video Codec SDK 接口代际；先核对版本，补丁需限于所用分支 |
| `WITH_NVCUVID` 未出现 | 检测日志与实际 SDK / 驱动库发现路径 |
| C++ 能运行、Python 不能导入 | Python 包安装位置、ABI、解释器和动态库路径 |
| 修改版本后仍链接旧库 | CMake cache、安装前缀和应用运行时搜索顺序 |

原文包含复制 SDK stub 到系统库目录的做法及随后 FFmpeg 出错记录。SDK stub 仅用于链接场景，不能覆盖真实驱动库或进入运行时搜索路径。

## Python、PyTorch 与 Libtorch

- 使用目标解释器的 `python -m pip`，项目有虚拟环境时直接复用。服务的解释器绝对路径必须指向同一环境；原文记录了用户安装包与 root 服务看不到同一 site-packages 的问题。
- Python 源码编译前准备 zlib、OpenSSL、xz 等所需开发依赖；使用独立前缀，不替换操作系统依赖的 Python。
- PyTorch 的 torch / torchvision / torchaudio、Python ABI、CPU / CUDA 构建需成套选择。原文包含不同版本组合，不能将其拼成一份依赖文件。
- 离线经验是先下载 wheel 及依赖，再从本地安装。尽量在匹配目标的环境收集；跨平台下载须指定实际平台 / ABI 并处理源码包依赖。

```sh
python -m pip download --dest "$WHEEL_DIR" -r "$REQUIREMENTS_FILE"
python -m pip install --no-index --find-links "$WHEEL_DIR" -r "$REQUIREMENTS_FILE"
```

有 CUDA 专用索引时同时保留项目对应的索引配置。wheel 不支持平台时重新选择正确产物或编译，不能改名掩盖不兼容。

原文 Jetson 的 Libtorch 来自已安装 torch 包的 `lib` 目录；路径应通过实际解释器定位，同时核对头文件、C++ ABI 和应用链接方式。桌面 x86_64 的 Libtorch 包不能直接用于 ARM。

## Qt 与常用 C++ 依赖

| 组件 | 可复用经验与适配规则 |
| --- | --- |
| Qt SDK | 显式选择项目的 qmake / kit；Linux GUI 依赖 X11 / OpenGL，服务环境另看插件和显示条件 |
| Qt MySQL 插件 | 使用应用相同 Qt 源码和 kit 构建 SQL driver；同时部署 `qsqlmysql` 插件与 MySQL 客户端库 |
| Qt 多媒体 / Charts | 原文含 Jetson 发行版包路径；缺开发包应解决依赖，不能任意伪造版本软链接 |
| QuaZip | 原文通过 `CMAKE_PREFIX_PATH` 选择 Qt；先对齐 Qt 主版本和该库的构建选项 |
| Boost | Linux bootstrap / b2；Windows 二进制或自编译要匹配工具集、架构和运行库 |
| yaml-cpp | 明确静态 / 动态；静态库进入共享对象时需要 PIC；选项名称按该版本 CMake 文件读取 |
| ZeroMQ / cppzmq | libzmq 提供库，cppzmq 提供 C++ 接口头；两者均应纳入依赖发现 |
| OpenSSL | 对齐消费方要求的 ABI；原文复制 so 到 Qt 的动作不是通用升级流程 |
| MongoDB C / C++ driver | 先 C driver / BSON，再 C++ driver / BSON C++；同前缀下发现，原文 Linux 页里的 `.dylib` 路径不能当成 Linux 产物 |
| Thrift | 编译器生成端和 C++ 运行库版本配套；Windows 手工改源码仅作旧 0.13.0 排错线索 |
| libevent / librdkafka | Windows 指定 x64 与 OpenSSL 等真实依赖；原文 librdkafka 页提及 OpenCV 路径属于需核实内容 |
| hiredis | 原文依赖归档 Windows Redis 分支及 Win32_Interop；仅用于指定旧项目，不能视为所有 Windows 项目的默认方案 |
| SQL Server | 原文只有安装 `msodbcsql17` 的短记录，需结合目标发行版与应用 ODBC 接口 |
| KDSoap / ONVIF | 用同一 Qt kit 构建 KDSoap；进一步见[视频接入](video.md) |

## 推理库

**tkDNN：** 原文前提为 CUDA 10.0、cuDNN 7.6.03、TensorRT 6.01、OpenCV、共享 yaml-cpp、Eigen3、CMake > 3.15。它记录了显式指定 `libnvinfer` 与 TensorRT include 的方法。复现时锁定 tkDNN 分支与整套依赖；新 TensorRT 不能直接假设兼容。`ENABLE_OPENCV_CUDA_CONTRIB` 与 hdf 模块应按实际应用需求配置。

**Paddle：** 原文围绕 C++ inference library 构建，包含 GPU、关闭 Python / MKL / NCCL、TensorRT 等开关。读取所选版本真实选项及产物目录；原文 `-WITH_TENSORRT` 缺 `D`，不要直接抄整条命令。

**SeetaFace：** 原文区分 x64 与 ARM GPU 构建，涉及 `PLATFORM`、`TS_USE_CUDA`、`TS_USE_CUBLAS`、`TS_ON_ARM`。先找到项目对应脚本和版本；示例把 `HOME` 当工作变量的写法应改成专用变量，不能覆盖用户环境。

## Windows 与 macOS

Windows：用目标 Qt kit 对应的 VS 开发者终端；明确 x86 / x64、Debug / Release、MSVC / MinGW、`/MD` / `/MT`。不要将所有依赖改成原文的 VS2015。CMake generator 按本机和项目实际工具集选择。

macOS：先确定 CPU 架构和编译目标；Homebrew 与 MySQL 前缀由本机定位。Qt SQL driver 需要匹配 Qt、客户端 dylib 和架构，发布时处理动态库加载路径；原文 `/usr/local` 并非所有 Mac 的固定路径。
