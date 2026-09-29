# 配套工具与有限资料入口

来源：`ansible/`、`jenkins/`、`jitsi/`、`android/`、`ios/`、`php/`、`雷达/`、`代码格式化/`；见[来源索引](source-index.md)。这些资料属于 CV 工程的辅助场景，不因使用本技能而自动部署。

## Ansible / Semaphore

原文记录 Ansible 安装、inventory 分组、连接探测，以及 Semaphore 的仓库、凭据、inventory、task template 配置。

适配时先复用项目已有 playbook 和目标主机分组，限定本次操作范围。Semaphore 的 SSH key、仓库权限与目标机凭据分别处理。服务配置路径取实际生成结果，不把源文的本机端口当作目标地址。

## Jenkins

原文是 macOS 上 Jenkins 的 launchctl 管理、JDK / Git / Maven 路径配置、码云 SSH 凭据和 Maven WAR 部署到 Tomcat。

- 从执行构建的 agent 环境定位工具；桌面用户的 PATH 不必然等同于 Jenkins 服务的 PATH。
- 公钥加入代码托管端，私钥由已有 Jenkins 凭据管理，不能提交进项目。
- 项目构建命令与测试策略由当前仓库决定；原文 `-Dmaven.test.skip=true` 不作为所有流水线默认值。
- 远程 Tomcat 管理访问使用项目指定账号和网络范围，不能为了让发布成功直接删除所有来源地址限制。
- 原文没有完整现代 Pipeline、签名或多平台构建配置；需要时结合现有 Jenkinsfile 和对应版本资料补充。

## Jitsi / Jibri

原文为 Ubuntu 20 环境，涉及 Prosody、Jicofo、Videobridge、Nginx、域名、TLS、BOSH、媒体端口；Jibri 只记录了 Chrome 与 ChromeDriver 版本对应关系。

按现有域名和部署版本整理端口、证书与反向代理，不硬编码原笔记的自定义端口。排查时区分网页可达、信令连接和媒体连通。安装源和签名采用目标版本官方步骤，不能保留下载时关闭证书检查的做法。

## Android

原文只有 Android Studio HTTP Proxy 与 Gradle 用户配置的经验。IDE 下载能联网而 Gradle 不能时，分别读取 IDE 代理与 `~/.gradle/gradle.properties`。关闭代理时只移除目标代理项，不清空整个文件。

没有 Android 原生 CV 推理 SDK、交叉编译或应用发布流程记录；此类任务读取项目已有 NDK / Gradle 配置及其所选 SDK 文档。

## iOS / CocoaPods

原文记录 `pod trunk register`、账户确认、podspec 检查和 `pod trunk push`，不包含 iOS 推理部署流程。

账户信息使用用户当前身份，不复制原文邮箱与姓名。检查规格、生成配置与公开发布区分处理；只有用户明确要求发布时才执行 trunk push。原文 `--allow-warnings` 不是忽略所有问题的默认选项。

## 雷达、PHP 与格式化

- `雷达/ubuntu.md` 只记录 Wireshark 安装；可作网络抓包工具入口，不能推断具体雷达协议、报文结构或驱动。抓包范围应对应实际接口和目标设备。
- PHP 原文是 Ubuntu Apache PHP 模块与 MySQL / curl / gd 依赖。按项目 PHP 版本和 Web 服务配置适配；面板安装不作为隐含操作。
- Uncrustify 原文记录 macOS Homebrew 安装及配置文件；只在项目选择该格式化工具时使用，保留仓库现有规则。

## 资料不足时

指出上游实际记录到哪一步，优先读目标项目、设备资料与所选版本官方文档。需要用户提供设备型号或接口说明时只询问缺少的事实，不将“有一个平台目录”描述成该平台所有工程场景都已覆盖。
