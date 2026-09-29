# 环境与平台

来源：`ubuntu/`、`qt/jetson/`、`qt/windows/qtsdk.md`、`qt/macos/`、`python/`。固定版本链接见[来源索引](source-index.md)。本文保留历史环境线索，命令按目标系统调整。

## 平台选择

| 平台 | 原笔记提供的经验 | 适配时的关键点 |
| --- | --- | --- |
| Ubuntu x86_64 | 16.04 / 18.04 / 20.04 / 22.04 的不同系统、驱动和编译记录 | 先识别发行版，再选软件源、包名和编译器 |
| Jetson Nano / TX2 / Xavier NX | JetPack 入口、USB / NVMe 根文件系统、Qt、PyTorch、风扇与功耗模式 | ARM64 与 L4T / JetPack 单独处理，不能套用桌面 NVIDIA 安装包 |
| CentOS | FFmpeg、数据库、Redis、JDK / Tomcat，包含 el7 包 | 固定目标发行版与架构；旧第三方源只作为复现线索 |
| Windows | Qt MSVC / MinGW、C++ 库、FFmpeg CUDA、服务和打包 | 位数、MSVC 工具集、运行库、Qt kit 保持一致 |
| macOS | Qt 数据库插件、MongoDB 驱动、yaml-cpp、ZeroMQ、Jenkins | 原路径主要为旧 Intel 环境；先识别 arm64 / x86_64 和实际工具前缀 |
| 树莓派 | Ubuntu 镜像、SSH、Netplan Wi-Fi | 确认型号与系统位数；没有完整 GPU 推理方案记录 |
| RK3399 | 厂商刷机入口和设备识别操作、SSH | 确认具体开发板；原文不提供完整 NPU / 推理 SDK 流程 |
| Android / iOS | Android Studio / Gradle 代理、CocoaPods | 只在 CV 项目的移动配套任务中使用，见[配套工具](tools.md) |

## 环境信息读取

Linux 按需读取 `/etc/os-release`、`uname -m`、`uname -r`，以及相关工具的 `--version`。Windows 可用 PowerShell 的系统信息和 `Get-Command` 定位工具，MSVC 信息在项目对应的开发者终端读取。macOS 用 `sw_vers`、`uname -m` 和实际 Homebrew 前缀。

**NVIDIA 桌面 GPU：** 对照 `nvidia-smi`、`/proc/driver/nvidia/version`、`nvcc --version` 与项目指定 CUDA 路径。`nvidia-smi` 的 CUDA 显示不能代替 Toolkit 安装版本。分别记录驱动、Toolkit、cuDNN、TensorRT。

**Jetson：** 优先读取 `/etc/nv_tegra_release` 和已安装 L4T 包，按需使用已有的 `tegrastats`、`jtop` 或 `nvpmodel --query`。原文指出 TX2 不用 `nvidia-smi` 查看 GPU；不能将该命令缺失直接判断为驱动坏了。

## NVIDIA 与 CUDA

原笔记包括 runfile 和包管理器安装路径，以及 CUDA 10.1、cuDNN 7.6.5、TensorRT 6.0.1.5 的历史组合。重建旧项目时先核对项目是否确实要求这些版本。

适配规则：

- 已有可用驱动时，将驱动更新与 Toolkit 安装分开决策。优先沿用该机器现有的管理方式。
- cuDNN / TensorRT 需匹配目标 CUDA、系统、架构与 Python ABI；路径在当前项目或服务环境中显式指定。
- `Failed to initialize NVML: Driver/library version mismatch`：先比较已加载内核模块与用户态库，查近期升级及重启情况。原文的批量卸载命令不是默认修复。
- `CUDA initialization failure ... 999`：记录占用 GPU 的进程和驱动日志。原文提到重载 `nvidia_uvm`，这会影响运行中的 GPU 工作，需先确认适用性和操作范围。
- `nomodeset`、禁用 nouveau、停显示管理器是原文特定安装故障的手段，只在对应启动或安装问题中评估。

## Jetson 的特殊边界

- 原文 PyTorch 安装依赖 NVIDIA 提供的 Jetson wheel，带 `aarch64` 和 Python ABI 标记。版本以目标 JetPack 对应资料为准。
- 原文 Qt 使用发行版 Qt 5 包及 `libqt5sql5-mysql` / `libqt5sql5-odbc`；包是否存在由目标发行版决定。
- rootOnUSB / rootOnNVMe 涉及分区、格式化、复制根文件系统及启动配置，只在用户要求迁移启动存储时处理。源文中的 `/dev/sda`、`/dev/nvme0n1` 必须重新识别。
- 风扇 sysfs 节点和功耗模式编号跟随具体板卡与系统；不能将 Xavier NX 的值用作所有 Jetson 的默认值。
- JDK、动态库和依赖包应使用 ARM 对应版本；原文的 `aarch64-linux-gun` 是路径拼写问题，使用目标机实际目录。

## 网络、远程与存储

原文覆盖 Netplan、NetworkManager、旧 `/etc/network/interfaces`、SSH、VNC、Privoxy 和 systemd 挂载。

- 先确定实际管理网络的组件，再修改它管理的配置。远程任务修改网卡前保留恢复路径；不要同时改三套网络配置。
- SSH 使用现有授权方式；不会因原文示例而打开 root 远程登录。代理地址和端口从目标环境取得。
- shell 代理、IDE 代理、包管理器代理可能独立，下载失败时定位实际请求进程。
- 应用数据目录挂载须与服务启动顺序一致；路径决定 systemd mount unit 的名称。
- 离线 deb / rpm 必须对应目标发行版、架构和依赖闭包。下载机已安装的包可能让下载集合不完整，不能把本机包列表视为目标完整依赖。

## 历史源与未知版本

源文含固定 `focal` 软件源、CentOS Nux 源和旧驱动 PPA。先匹配目标系统，再查该版本的官方安装说明。不为满足旧 `libjasper-dev`、`qt5-default` 等包名混入其他发行版仓库。没有联网条件时，保留版本适配待办，不宣称安装可行。
