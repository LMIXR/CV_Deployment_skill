# helpfile 来源索引

## 来源与用法

- 仓库：[LMIXR/helpfile](https://github.com/LMIXR/helpfile)。
- 固定提交：[`db013a05ed08d29fdab01a684176af866e5ee565`](https://github.com/LMIXR/helpfile/commit/db013a05ed08d29fdab01a684176af866e5ee565)。
- 上游提交时间：2026-09-29T07:31:48Z；整理日期：2026-09-29。
- 此处是原始经验的可追溯入口；整理后的六份参考资料可离线使用，原文全文按需在线读取。
- 原文版本号、路径和命令是当时环境记录，不表示当前版本仍适用，也不是已执行的验证证据。
- 只在需要原始参数、旧错误或特殊平台细节时打开对应链接；无需通读全部目录。
- 原始脚本和配置仅供阅读适配；没有作为可执行文件随技能分发。旧口令、个人地址和路径没有迁入技能。
- 不纳入原仓库的其他 agent 技能、字体、宣传图片、截图、预编译程序；保留其工程笔记、脚本和配置的来源链接。

共索引 119 个工程文本文件。

## 常用检索线索

| 任务 / 错误 | 查找原始路径 |
| --- | --- |
| 驱动版本冲突、CUDA 初始化 | `ubuntu/显卡环境.md`、`ubuntu/cuda.md` |
| JetPack、NVMe、ARM Qt | `ubuntu/Jetson*`、`qt/jetson/` |
| OpenCV contrib 下载或 NVCUVID | `qt/ubuntu/opencv.md` |
| NVENC 编译、GStreamer 插件 | `qt/ubuntu/ffmpeg.md`、`qt/ubuntu/gst-rtsp-server.md` |
| MSVC / DLL / Qt kit | `qt/windows/` |
| macOS dylib / MySQL 插件 | `qt/macos/` |
| WVP、RTP、公网播放 | `流媒体/GB28181.md` |
| systemd、PID、打包 | `qt/ubuntu/打包/`、`流媒体/` |
| 离线包 / wheel | `ubuntu/包.md`、`python/`、`mysql/` |

## Ubuntu 与边缘设备

整理后的入口：[Ubuntu 与边缘设备](platforms.md)。

- [ubuntu/JetsonNano.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/ubuntu/JetsonNano.md) — 笔记
- [ubuntu/JetsonXavierNX.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/ubuntu/JetsonXavierNX.md) — 笔记
- [ubuntu/cuda.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/ubuntu/cuda.md) — 笔记
- [ubuntu/rockrk3399.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/ubuntu/rockrk3399.md) — 笔记
- [ubuntu/ssh配置.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/ubuntu/ssh%E9%85%8D%E7%BD%AE.md) — 笔记
- [ubuntu/vnc.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/ubuntu/vnc.md) — 笔记
- [ubuntu/代理.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/ubuntu/%E4%BB%A3%E7%90%86.md) — 笔记
- [ubuntu/包.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/ubuntu/%E5%8C%85.md) — 笔记
- [ubuntu/显卡环境.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/ubuntu/%E6%98%BE%E5%8D%A1%E7%8E%AF%E5%A2%83.md) — 笔记
- [ubuntu/更换源.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/ubuntu/%E6%9B%B4%E6%8D%A2%E6%BA%90.md) — 笔记
- [ubuntu/树莓派.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/ubuntu/%E6%A0%91%E8%8E%93%E6%B4%BE.md) — 笔记
- [ubuntu/系统.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/ubuntu/%E7%B3%BB%E7%BB%9F.md) — 笔记
- [ubuntu/网卡.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/ubuntu/%E7%BD%91%E5%8D%A1.md) — 笔记
- [ubuntu/脚本/auto-del-dir.sh](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/ubuntu/%E8%84%9A%E6%9C%AC/auto-del-dir.sh) — 脚本 / 配置
- [ubuntu/脚本/auto-del-disk.sh](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/ubuntu/%E8%84%9A%E6%9C%AC/auto-del-disk.sh) — 脚本 / 配置
- [ubuntu/脚本/auto-del-file.sh](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/ubuntu/%E8%84%9A%E6%9C%AC/auto-del-file.sh) — 脚本 / 配置
- [ubuntu/脚本/auto-del-log.sh](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/ubuntu/%E8%84%9A%E6%9C%AC/auto-del-log.sh) — 脚本 / 配置

## Qt 与跨平台 C++

整理后的入口：[Qt 与跨平台 C++](build.md)。

- [qt/centos/ffmpeg.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/centos/ffmpeg.md) — 笔记
- [qt/jetson/mysql.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/jetson/mysql.md) — 笔记
- [qt/jetson/qt.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/jetson/qt.md) — 笔记
- [qt/macos/mongodb.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/macos/mongodb.md) — 笔记
- [qt/macos/mysql.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/macos/mysql.md) — 笔记
- [qt/macos/yamlcpp.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/macos/yamlcpp.md) — 笔记
- [qt/macos/zeromq.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/macos/zeromq.md) — 笔记
- [qt/ubuntu/boost.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/ubuntu/boost.md) — 笔记
- [qt/ubuntu/charts.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/ubuntu/charts.md) — 笔记
- [qt/ubuntu/ffmpeg.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/ubuntu/ffmpeg.md) — 笔记
- [qt/ubuntu/gcc.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/ubuntu/gcc.md) — 笔记
- [qt/ubuntu/gst-rtsp-server.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/ubuntu/gst-rtsp-server.md) — 笔记
- [qt/ubuntu/media.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/ubuntu/media.md) — 笔记
- [qt/ubuntu/mongodb.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/ubuntu/mongodb.md) — 笔记
- [qt/ubuntu/mysql.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/ubuntu/mysql.md) — 笔记
- [qt/ubuntu/onvif.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/ubuntu/onvif.md) — 笔记
- [qt/ubuntu/opencv.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/ubuntu/opencv.md) — 笔记
- [qt/ubuntu/openssl.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/ubuntu/openssl.md) — 笔记
- [qt/ubuntu/qtsdk.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/ubuntu/qtsdk.md) — 笔记
- [qt/ubuntu/quazip.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/ubuntu/quazip.md) — 笔记
- [qt/ubuntu/seetaface.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/ubuntu/seetaface.md) — 笔记
- [qt/ubuntu/sqlserver.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/ubuntu/sqlserver.md) — 笔记
- [qt/ubuntu/thrift.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/ubuntu/thrift.md) — 笔记
- [qt/ubuntu/yamlcpp.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/ubuntu/yamlcpp.md) — 笔记
- [qt/ubuntu/zeromq.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/ubuntu/zeromq.md) — 笔记
- [qt/ubuntu/打包/init-server/server.sh](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/ubuntu/%E6%89%93%E5%8C%85/init-server/server.sh) — 脚本 / 配置
- [qt/ubuntu/打包/pack.sh](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/ubuntu/%E6%89%93%E5%8C%85/pack.sh) — 脚本 / 配置
- [qt/ubuntu/打包/systemctl-server/monitor.sh](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/ubuntu/%E6%89%93%E5%8C%85/systemctl-server/monitor.sh) — 脚本 / 配置
- [qt/ubuntu/打包/systemctl-server/restart.sh](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/ubuntu/%E6%89%93%E5%8C%85/systemctl-server/restart.sh) — 脚本 / 配置
- [qt/ubuntu/打包/systemctl-server/server.service](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/ubuntu/%E6%89%93%E5%8C%85/systemctl-server/server.service) — 脚本 / 配置
- [qt/ubuntu/打包/systemctl-server/start.sh](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/ubuntu/%E6%89%93%E5%8C%85/systemctl-server/start.sh) — 脚本 / 配置
- [qt/ubuntu/打包/systemctl-server/stop.sh](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/ubuntu/%E6%89%93%E5%8C%85/systemctl-server/stop.sh) — 脚本 / 配置
- [qt/ubuntu/打包/可执行文件.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/ubuntu/%E6%89%93%E5%8C%85/%E5%8F%AF%E6%89%A7%E8%A1%8C%E6%96%87%E4%BB%B6.md) — 笔记
- [qt/ubuntu/打包/打包.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/ubuntu/%E6%89%93%E5%8C%85/%E6%89%93%E5%8C%85.md) — 笔记
- [qt/windows/boost.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/windows/boost.md) — 笔记
- [qt/windows/cmake.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/windows/cmake.md) — 笔记
- [qt/windows/ffmpeg.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/windows/ffmpeg.md) — 笔记
- [qt/windows/kafka.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/windows/kafka.md) — 笔记
- [qt/windows/libevent.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/windows/libevent.md) — 笔记
- [qt/windows/mongodb.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/windows/mongodb.md) — 笔记
- [qt/windows/mysql.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/windows/mysql.md) — 笔记
- [qt/windows/onvif.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/windows/onvif.md) — 笔记
- [qt/windows/qtsdk.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/windows/qtsdk.md) — 笔记
- [qt/windows/redis.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/windows/redis.md) — 笔记
- [qt/windows/thrift.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/windows/thrift.md) — 笔记
- [qt/windows/yamlcpp.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/windows/yamlcpp.md) — 笔记
- [qt/windows/打包.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/windows/%E6%89%93%E5%8C%85.md) — 笔记
- [qt/添加组件.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/qt/%E6%B7%BB%E5%8A%A0%E7%BB%84%E4%BB%B6.md) — 笔记

## Python 与 PyTorch

整理后的入口：[Python 与 PyTorch](build.md)。

- [python/opencv.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/python/opencv.md) — 笔记
- [python/pytorch.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/python/pytorch.md) — 笔记
- [python/ubuntu.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/python/ubuntu.md) — 笔记

## Paddle

整理后的入口：[Paddle](build.md)。

- [paddle/ubuntu.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/paddle/ubuntu.md) — 笔记

## tkDNN

整理后的入口：[tkDNN](build.md)。

- [tkdnn/ubuntu.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/tkdnn/ubuntu.md) — 笔记

## GB28181 与媒体服务

整理后的入口：[GB28181 与媒体服务](video.md)。

- [流媒体/GB28181.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/%E6%B5%81%E5%AA%92%E4%BD%93/GB28181.md) — 笔记
- [流媒体/wvp/auto-del-log.sh](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/%E6%B5%81%E5%AA%92%E4%BD%93/wvp/auto-del-log.sh) — 脚本 / 配置
- [流媒体/wvp/logrotate-wvp](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/%E6%B5%81%E5%AA%92%E4%BD%93/wvp/logrotate-wvp) — 脚本 / 配置
- [流媒体/wvp/start.sh](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/%E6%B5%81%E5%AA%92%E4%BD%93/wvp/start.sh) — 脚本 / 配置
- [流媒体/wvp/stop.sh](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/%E6%B5%81%E5%AA%92%E4%BD%93/wvp/stop.sh) — 脚本 / 配置
- [流媒体/wvp/wvp.service](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/%E6%B5%81%E5%AA%92%E4%BD%93/wvp/wvp.service) — 脚本 / 配置
- [流媒体/zlmedia/start.sh](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/%E6%B5%81%E5%AA%92%E4%BD%93/zlmedia/start.sh) — 脚本 / 配置
- [流媒体/zlmedia/stop.sh](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/%E6%B5%81%E5%AA%92%E4%BD%93/zlmedia/stop.sh) — 脚本 / 配置
- [流媒体/zlmedia/zlmedia.service](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/%E6%B5%81%E5%AA%92%E4%BD%93/zlmedia/zlmedia.service) — 脚本 / 配置

## Docker 与容器服务

整理后的入口：[Docker 与容器服务](deployment.md)。

- [docker/docker.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/docker/docker.md) — 笔记
- [docker/elk.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/docker/elk.md) — 笔记
- [docker/mysql.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/docker/mysql.md) — 笔记
- [docker/portainer.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/docker/portainer.md) — 笔记
- [docker/redis.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/docker/redis.md) — 笔记
- [docker/swarm.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/docker/swarm.md) — 笔记
- [docker/tomcat.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/docker/tomcat.md) — 笔记

## Windows 服务

整理后的入口：[Windows 服务](deployment.md)。

- [windows/服务.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/windows/%E6%9C%8D%E5%8A%A1.md) — 笔记

## Nginx

整理后的入口：[Nginx](deployment.md)。

- [nginx/windows/nginx-service.exe.config](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/nginx/windows/nginx-service.exe.config) — 脚本 / 配置
- [nginx/windows/nginx-service.xml](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/nginx/windows/nginx-service.xml) — 脚本 / 配置
- [nginx/windows/nginx.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/nginx/windows/nginx.md) — 笔记

## MySQL

整理后的入口：[MySQL](services.md)。

- [mysql/centos.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/mysql/centos.md) — 笔记
- [mysql/ubuntu.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/mysql/ubuntu.md) — 笔记
- [mysql/windows.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/mysql/windows.md) — 笔记
- [mysql/主从复制.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/mysql/%E4%B8%BB%E4%BB%8E%E5%A4%8D%E5%88%B6.md) — 笔记

## MongoDB

整理后的入口：[MongoDB](services.md)。

- [mongo/centos.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/mongo/centos.md) — 笔记
- [mongo/ubuntu.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/mongo/ubuntu.md) — 笔记

## Redis

整理后的入口：[Redis](services.md)。

- [redis/centos.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/redis/centos.md) — 笔记
- [redis/ubuntu.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/redis/ubuntu.md) — 笔记

## MinIO

整理后的入口：[MinIO](services.md)。

- [minio/ubuntu.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/minio/ubuntu.md) — 笔记

## Kafka

整理后的入口：[Kafka](services.md)。

- [kafka/ubuntu.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/kafka/ubuntu.md) — 笔记
- [kafka/windows.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/kafka/windows.md) — 笔记

## Flume

整理后的入口：[Flume](services.md)。

- [flume/windows.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/flume/windows.md) — 笔记

## Tomcat

整理后的入口：[Tomcat](services.md)。

- [tomcat/centos.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/tomcat/centos.md) — 笔记
- [tomcat/tomcat.service](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/tomcat/tomcat.service) — 脚本 / 配置
- [tomcat/tomcatnx.service](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/tomcat/tomcatnx.service) — 脚本 / 配置
- [tomcat/ubuntu.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/tomcat/ubuntu.md) — 笔记

## Ansible 与 Semaphore

整理后的入口：[Ansible 与 Semaphore](tools.md)。

- [ansible/semaphore.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/ansible/semaphore.md) — 笔记
- [ansible/安装.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/ansible/%E5%AE%89%E8%A3%85.md) — 笔记

## Jenkins

整理后的入口：[Jenkins](tools.md)。

- [jenkins/安装.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/jenkins/%E5%AE%89%E8%A3%85.md) — 笔记
- [jenkins/码云.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/jenkins/%E7%A0%81%E4%BA%91.md) — 笔记
- [jenkins/配置.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/jenkins/%E9%85%8D%E7%BD%AE.md) — 笔记
- [jenkins/项目.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/jenkins/%E9%A1%B9%E7%9B%AE.md) — 笔记

## Jitsi

整理后的入口：[Jitsi](tools.md)。

- [jitsi/ubuntu.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/jitsi/ubuntu.md) — 笔记

## Android

整理后的入口：[Android](tools.md)。

- [android/代理.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/android/%E4%BB%A3%E7%90%86.md) — 笔记

## iOS

整理后的入口：[iOS](tools.md)。

- [ios/pod.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/ios/pod.md) — 笔记

## PHP

整理后的入口：[PHP](tools.md)。

- [php/ubuntu.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/php/ubuntu.md) — 笔记

## 雷达工具

整理后的入口：[雷达工具](tools.md)。

- [雷达/ubuntu.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/%E9%9B%B7%E8%BE%BE/ubuntu.md) — 笔记

## Uncrustify

整理后的入口：[Uncrustify](tools.md)。

- [代码格式化/uncrustify/defaults.cfg](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/%E4%BB%A3%E7%A0%81%E6%A0%BC%E5%BC%8F%E5%8C%96/uncrustify/defaults.cfg) — 脚本 / 配置
- [代码格式化/uncrustify/macos.md](https://github.com/LMIXR/helpfile/blob/db013a05ed08d29fdab01a684176af866e5ee565/%E4%BB%A3%E7%A0%81%E6%A0%BC%E5%BC%8F%E5%8C%96/uncrustify/macos.md) — 笔记
