# 视频接入

来源：`qt/ubuntu/ffmpeg.md`、`qt/windows/ffmpeg.md`、`qt/centos/ffmpeg.md`、`qt/ubuntu/gst-rtsp-server.md`、`qt/ubuntu/media.md`、`qt/*/onvif.md`、`流媒体/GB28181.md` 及服务脚本；见[来源索引](source-index.md)。

## 先明确数据路径

区分以下环节，再定位用户要改变的部分：

```text
摄像头 / 视频文件 → 协议接入 → 解复用 / 解码 → 图像处理或推理 → 显示 / 录像 / 转发
```

记录协议、视频编码、像素格式、分辨率、帧率、音频需求、目标输出及网络路径。ONVIF 管理与取流信息、RTSP 媒体会话、GB28181 信令和 RTP 媒体分开处理。设备注册成功或端口开放都不能单独说明画面可用。

已有视频管线时先定位实际使用的是 FFmpeg、GStreamer 还是 Qt 后端。用户未要求换框架时保留现有技术栈。

## FFmpeg 编译

原文桌面 NVIDIA 构建关系为：汇编工具 / 编码库 → nv-codec-headers → FFmpeg。仅安装当前功能需要的库。

- x264 / x265 用于相应软件编码需求；仅解码或流复制不自动要求重新编译它们。
- `PKG_CONFIG_PATH` 指向依赖前缀的 `lib/pkgconfig`。头文件、链接库、运行时库三条路径分别处理。
- 原文包含 FFmpeg 3.4.8 / 4.3.1、nv-codec-headers 9.1、x264 152 的组合记录；它们是旧项目线索，不能据此断言其他版本都不兼容。
- `nvenc requested but not found` 先看 configure 日志，定位 headers、API 版本、驱动要求及工具链。不要先重装整个 CUDA。
- 选择共享 / 静态、CUDA / NVENC / CUVID / NPP 等选项时读取该版本帮助和构建约束。原文 `--enable-gpl`、`--enable-nonfree` 由所选依赖与发布要求决定，不能无条件加上。
- 原文把库复制到全局目录解决加载问题；整理后优先使用独立安装前缀和应用运行环境，避免旧、新 libav 混载。

**Windows：** 原文从 VS x64 开发者终端启动 MSYS2 以继承 MSVC 环境，再安装构建工具和 nv-codec-headers，以 `--toolchain=msvc` 构建。先明确需要 MSVC 还是 MinGW 产物；MSYS2 作为 shell 不代表最终产物使用同一 ABI。CUDA include / lib 路径取实际安装位置。原文还记录旧 VS 环境 `D8000` 与语言设置的问题，只在对应错误出现时调查。

**CentOS：** 原文走 el7 EPEL / Nux 的 FFmpeg 包。需先识别目标版本及仓库可用性，不复制旧源命令到其他发行版。

**Jetson：** 不把桌面 NVENC / CUVID 编译方式当成所有 Jetson 的硬件视频接口。根据 L4T、设备能力及其提供的多媒体组件选择实现。

## GStreamer 与 RTSP server

原文包含 gst-rtsp-server 1.14.4 / GStreamer 1.14.5，以及 Ubuntu 22 上 GLib、GStreamer 运行库、开发包和插件组的准备经验。

1. 分别识别运行时版本、开发包版本、所编译 rtsp-server / 插件版本。
2. 缺 `gstreamer-1.0.pc` 时查开发包和 pkg-config 搜索路径；安装运行库不等于安装开发包。
3. 按管线需要选择 base / good / bad / ugly / libav 插件。H.264 管线缺 x264 时，定位插件而不是仅检查系统 libx264。
4. 原文旧 NVIDIA 插件从相同版本 `gst-plugins-bad` 的 `sys/nvenc` / `sys/nvdec` 构建。目录和构建系统需以选定版本为准，不能对新版固定执行 `autogen.sh`。
5. 插件安装到自定义路径时，应用及服务的 `GST_PLUGIN_PATH` 必须能找到它。终端环境不会自动传给 systemd。

用户要求诊断时，可以用已有 `gst-inspect-1.0` 查询目标元素和加载错误。只有管线实际使用时才检查相关插件，不全量重装插件集合。

## ONVIF / KDSoap

原文主要记录 KDSoap 编译：Ubuntu 上指定 qmake、构建共享库、设置动态库搜索路径；Windows 上在 VS 控制台运行 configure / nmake。

适配时保持 KDSoap 与应用 Qt kit / 编译器一致。原文复制私有头文件是特定 KDSoap 1.8.0 的历史做法，先确认项目是否真正依赖该接口。仓库没有完整的 ONVIF 设备发现、认证、Profile / URI 获取实现；涉及这些任务时读取应用实现与目标设备文档。

## GB28181：WVP + ZLMediaKit

原文中 WVP 管理设备与信令，ZLMediaKit 处理媒体；Redis、JDK、FFmpeg 是该记录里的配套组件。不同 WVP 版本的其他依赖由其项目配置决定。

部署关系：

1. 识别现有 WVP 与 ZLMediaKit 版本、配置文件和启动方式。
2. WVP 配置 Redis、SIP 参数、Web 服务地址及媒体服务器连接；原文使用 jar 同目录的外置 `application.yml`。
3. ZLMediaKit 获取子模块后构建；明确实际二进制目录、`config.ini`、FFmpeg 路径和各协议监听端口。
4. 公网环境分别处理信令监听、媒体端口、宣告地址与 NAT 映射。Web 页面可达不代表 SIP / RTP 数据路径正常。
5. 沿用版本实际提供的设备、点播和播放 API。原文的 `/api/devices`、`/api/play/{deviceId}/{channelId}` 与十六进制 stream id 是旧实现线索，不能把它们当成所有版本的接口契约。

WVP 与 ZLMediaKit 的服务管理见[部署](deployment.md)。不要执行原启动脚本中并列的 Ubuntu16 / Ubuntu18 两条启动示例，以免重复启动。

## 按症状缩小范围

| 现象 | 要区分的原因 |
| --- | --- |
| RTSP 连接失败 | 目标地址、凭据、端口、路径、服务状态、路由 |
| 有连接但无媒体 | 协商的传输方式、RTP / RTCP 端口、NAT、媒体超时 |
| 有数据但无法解码 | 编码类型、关键帧 / 参数集、解码器是否存在、硬件是否支持输入格式 |
| 软件解码可用、硬件失败 | 驱动与运行库、实际加载的 SDK 库、设备能力、硬件上下文 |
| 命令行能播、Qt 不能播 | Qt kit、媒体插件、运行环境、应用管线参数 |
| WVP 注册成功但播放失败 | SIP 点播结果、ZLMediaKit 收流、媒体端口映射、播放协议路径 |
| 长时间运行积压或延迟 | 应用队列、处理速率、时间戳、丢帧策略和重连逻辑 |

原文提供切片录像、定时截图、图片合视频等 FFmpeg 示例。生成命令时使用用户指定输出目录，确定覆盖行为和空间预算；不会为接入任务自动启用永久录像。用户跳过验证时不主动拉摄像头流或创建录像。
