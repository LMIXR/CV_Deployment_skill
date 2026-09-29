# 打包与部署

来源：`qt/ubuntu/打包/`、`qt/windows/打包.md`、`windows/服务.md`、`nginx/windows/`、`docker/`、`流媒体/`、`ubuntu/脚本/`、`tomcat/`；见[来源索引](source-index.md)。

## 应用目录与运行环境

先识别应用二进制、配置、动态库、插件、模型和数据目录；部署路径、服务名、监听端口与用户现有接口保持一致。

可在新项目使用 `bin/`、`lib/`、`plugins/`、`config/` 分离产物；已有项目优先沿用原布局。将日志、录像和可变数据放到明确的可写目录，避免升级二进制时覆盖数据。

运行时至少需要匹配架构、编译器运行库、Qt kit 和第三方库 ABI。构建目录能启动不代表拷到其他机器后仍有完整依赖。

## Linux / Qt 打包

原文 `pack.sh` 根据 `ldd` 列出并复制共享库。该方法提供初步依赖线索，但不覆盖延迟加载插件、Qt 插件、模型、配置和所有驱动运行时。

- 对可信的自身构建产物分析动态依赖，区分要随包分发的库和目标主机提供的驱动 / 系统组件。
- Qt SQL driver 放在对应插件目录，还要包含其客户端库。例如 `libqsqlmysql.so` 仍依赖 `libmysqlclient.so`。
- GUI / 多媒体程序另考虑 platform、imageformats、GStreamer 等实际用到的插件及其间接依赖。
- 使用应用自己的运行路径配置、合适的 RPATH 或服务环境。原文 `/etc/ld.so.conf.d/` 与 `ldconfig` 属于全局方案，只在确需系统级安装时采用。
- 诊断插件时可在限定的启动环境启用 `QT_DEBUG_PLUGINS=1`，记录失败库路径；不要永久向全系统注入另一套 Qt 库路径。
- `.desktop` 的 `Exec`、`Icon` 指向实际应用位置；图形会话自启动与后台 systemd 服务是不同需求。原文 `-no-pie` 属于特定桌面启动经验，不作为所有程序的构建默认值。

## systemd

先确认进程是否前台运行、是否自己派生守护进程，再选择 unit 类型。

原文 shell 包装器通过后台进程、PID 文件和 `Type=forking` 管理服务。新的前台程序可直接交给 systemd 管理；旧程序有兼容要求时保留接口并修正 PID 归属和退出处理。不要使用进程名模糊匹配停止其他实例。

下面是供生成项目文件时改写的前台服务形状，尖括号均需替换，不直接安装此段：

```ini
[Unit]
Description=CV application
After=network.target

[Service]
Type=simple
User=<service-user>
WorkingDirectory=<absolute-app-directory>
ExecStart=<absolute-executable> <application-arguments>
Restart=on-failure
RestartSec=5s

[Install]
WantedBy=multi-user.target
```

- 配置明确的工作目录、运行用户、环境与可写目录。依赖存储挂载时可按实际情况增加 `RequiresMountsFor=`；确需网络就绪时处理 online target 及目标机网络管理器。
- systemd 不会自动读取交互 shell 的 `.bashrc`；CUDA、Python、GStreamer、Qt 依赖路径应在服务环境明确表达。
- Java 属性参数位于 `-jar` 前：`java -Dspring.config.location=<config> -jar <application.jar>`；具体 Spring 参数语义以项目版本为准。
- WVP 原文同时含前台和后台启动方式、旧 PermGen 参数及固定约 3.5 GiB 堆大小。按目标 JDK、内存与服务类型重写，不逐行照搬。
- 停止服务优先走程序和服务管理器的正常退出路径；原文 `kill -9` 不作为普通停止方式。

生成 unit 与实际启用服务分开处理。任务授权部署时执行所需安装、daemon reload 和启动；只有用户要求开机启动时或任务已明确包含自启动才 enable。记录实际操作，不把生成配置描述成服务已经运行。

## Windows 与 macOS

**Windows Qt：** 使用构建应用的同一 kit 的 `windeployqt`；额外带上实际第三方 DLL，例如 MySQL 客户端。按需用 MSVC `dumpbin /dependents` 定位缺依赖；匹配架构、工具集和运行库。

**Windows 服务：** 原文记录 SrvanyUI 包装 Java，以及 Nginx service wrapper 的 XML。生成配置时指定程序、参数、工作目录、服务账户、日志目录与停止命令；不要直接分发仓库中的旧 `nginx-service.exe` 作为可信新安装器。

**macOS：** 原文集中于动态库构建和 Jenkins launchctl，缺完整 Qt 发布流程。先读取项目实际 bundle / 安装方案，需要新的发布步骤时补充该版本官方资料，不能声称源仓库已有完整签名、公证流程。

## Docker

原文包括 Docker CE、Swarm、Portainer、MySQL、Redis、Tomcat 和 ELK。

- 保留项目已有镜像和编排方式；版本 / digest、CPU 架构、数据卷、配置挂载、端口和启动参数显式化。
- Ubuntu 安装源中的 `arch=amd64` 只适用于对应架构；不能直接移到 Jetson。旧 `apt-key` 命令以目标版本官方安装流程替换。
- 容器部署仍依赖主机 GPU 驱动；原文没有完整 NVIDIA 容器运行时配置，不补造已支持的版本组合。
- 数据库的 data / logs / conf 卷按实际服务拆分。账号口令由已有凭据机制提供，不复制原文 `docker run` 中的密码。
- ELK 的 `vm.max_map_count` 是特定组件的系统参数，只有部署该组件且版本需要时才调整。
- 原文 Swarm 使用 docker-machine / VirtualBox，只作为旧环境复现资料；已有真实节点不需要照着新建虚拟机。
- Portainer 的 Docker socket 挂载属于管理访问，只在请求部署该管理组件时设置。

## 日志和录像保留

原文提供按时间删除文件、按磁盘阈值清理、cron、logrotate 和端口监控重启脚本。

按实际保留需求选择一个机制：日志轮转、文件年龄或目录容量。先确定目录边界、命名规则、保留时间 / 容量、正在写入的文件及磁盘满时行为。所有路径和阈值参数化；空路径、根目录和解析失败不能变成删除范围。

原文端口监控只能证明监听状态，不能代替视频或业务状态。用户没有要求自动重启时不新增定时重启。用户要求跳过验证时，只生成所需配置与说明，不对真实录像执行清理试验。
