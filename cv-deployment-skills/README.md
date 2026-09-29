# CV 工程部署技能

把 [LMIXR/helpfile](https://github.com/LMIXR/helpfile) 中的工程经验整理为 agent 可按任务读取的技能。

## 使用

源码目录为 [`cv-deploy/`](cv-deploy/SKILL.md)，调用名为 `$cv-deploy`。本项目的安装位置是 [`.agents/skills/cv-deploy/`](../.agents/skills/cv-deploy/SKILL.md)，供在本仓库工作的 agent 发现和使用。

修改源码后，将 `cv-deploy/` 中的技能文件同步到项目安装目录。新会话中可使用下面的调用示例；当前会话也可通过安装位置直接读取技能。

示例：

```text
$cv-deploy 为这台 Ubuntu 主机配置项目需要的 CUDA 和 OpenCV，先读取项目版本约束。
$cv-deploy 帮我编译 Windows MSVC 版本的 FFmpeg 并接入现有 Qt 工程。
$cv-deploy 排查 Jetson 上视频能连接但不能解码的问题。
$cv-deploy 把现有 WVP 和 ZLMediaKit 配置成服务，保留现有端口。
```

## 内容

- 环境与平台：Ubuntu、CentOS、Windows、macOS、Jetson、树莓派、RK3399，以及 Android / iOS 配套工具记录。
- 依赖编译：OpenCV、FFmpeg、GStreamer、Qt、CUDA、cuDNN、TensorRT、PyTorch、Paddle、tkDNN 和 C++ 库。
- 视频接入：RTSP、ONVIF、GB28181、WVP、ZLMediaKit。
- 部署：动态库与 Qt 插件、systemd、Windows 服务、Docker、数据库、消息服务和运维工具。

`SKILL.md` 是入口；`references/` 保存整理后的经验与适配规则；`references/source-index.md` 提供固定版本的上游来源。参考资料随技能分发，可离线阅读；需要原始全文时才访问上游链接。

## 来源与状态

来源固定为 helpfile 提交 `db013a05ed08d29fdab01a684176af866e5ee565`，整理日期为 2026-09-29。历史版本组合只是原笔记的适用线索，不能据此声称在其他版本上可用。资料覆盖全部原有平台，各平台资料深度不等。

按本次要求，先交付技能；未运行技能验收、行为测试、依赖编译或部署验证。没有复制原文中的账号口令、个人路径、预编译程序、图片或字体。

维护时先更新对应参考资料和来源链接，再调整入口。新的使用经验应记录环境条件和具体失败现象，避免把单次修复变成所有项目的固定步骤。
