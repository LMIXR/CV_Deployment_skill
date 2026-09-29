# 配套数据与消息服务

来源：`mysql/`、`mongo/`、`redis/`、`minio/`、`kafka/`、`flume/`、`tomcat/` 与相应 `docker/` 笔记；见[来源索引](source-index.md)。只有 CV 应用实际依赖某项服务时才引入。

## 共同决策

优先读应用已有连接配置，确定服务版本、网络地址、持久化目录、运行用户和认证方式。区分服务端安装、客户端工具、语言驱动与 Qt 插件；应用报告“driver not loaded”时不先重装数据库。

原文包含个人口令、root 远程授权及全网监听示例。生成配置时使用目标环境的专用账户与实际访问范围，保留现有权限设计。不会把重初始化数据目录当作通用启动修复。

## MySQL

- Ubuntu 原文分别记录 5.7、8.0 和 ARM64 离线包；CentOS 记录 el7 rpm；Windows 使用 ZIP、`my.ini` 和服务注册。不能混合不同大版本的系统表修改和认证命令。
- 离线依赖包括相应版本的 common、client / server core、客户端库、libaio、libmecab、libevent 等。版本、架构和发行版必须成套，不按源文重复或混杂的文件名机械下载。
- 数据目录迁移同时涉及所有权、AppArmor、挂载时机和服务配置。存在数据时采用实际迁移 / 备份方案；`--initialize` 仅属于已明确的新实例初始化。
- Qt MySQL 插件构建与部署见[依赖编译](build.md)，服务端可连接与 Qt 插件可加载分开定位。
- 复制记录基于 binlog 文件 / 位置：备份一致性与记录的位置必须对应。原文旧主从命令需要按目标版本和现有复制模式适配。
- CentOS 原文出现删除 MariaDB 依赖的步骤；先查看现有应用依赖与迁移需求，不将其当成安装 MySQL 的必做操作。

## MongoDB

- 原文包含 Ubuntu tar 包 / 服务和 CentOS 4.4 rpm，另有复制集、分片及导入导出记录。先区分 `mongod`、`mongos`、config server 和应用连接端点。
- 配置文件可能是旧键值格式或 YAML；只使用所选版本支持的形式。`fork` 行为应与 systemd 的进程类型一致。
- 数据与日志路径、监听地址、认证和 WiredTiger 内存设置按实例配置；原文 2 GiB / 512 MiB 是部署示例，不是统一限制。
- 启用认证涉及初始管理员和应用账户的创建顺序。复用原有认证数据库与角色，不在输出或文件中嵌入原文连接串口令。
- 导入 JSON 时区分目标数据库、collection、格式与是否覆盖现有数据；分片拓扑不是单实例启动故障的修复步骤。

## Redis

- 原文覆盖 Ubuntu 软件包、源码构建、CentOS rpm 和 systemd。源码安装产物可能依赖 jemalloc，打包需纳入实际动态依赖。
- RDB 与 AOF 是不同持久化配置：修改 `save` 不等于关闭 AOF，修改 `appendonly` 不等于关闭 RDB。依据应用的数据可丢失范围选择。
- `dir`、用户目录权限、日志目录及服务配置相互配套；前台 / daemon / supervised 模式以所选版本和 service 类型决定。
- `FLUSHDB` / `FLUSHALL` 是数据删除操作，只有任务明确要求清空对应范围时使用。

## MinIO

原文记录 data 目录、API 与控制台端口、环境文件配置。生成部署时设置现有凭据、卷目录权限、两个端口及服务账户；不因旧示例而把服务改为 root。具体发行包和环境变量以目标版本为准。

## Kafka 与 Flume

原文 Kafka 使用 ZooKeeper，包含 2.8.0 安装记录和 3.5.0 路径示例；Windows 用 bat 脚本。它不能说明其他版本仍使用相同元数据管理方式，先识别项目版本和现有部署模式。

- 分开配置绑定地址 `listeners` 与客户端可达的 `advertised.listeners`。跨网段能连接 bootstrap 端口却不能消费时，检查元数据返回的地址。
- 服务依赖、JDK、数据目录、SASL / JAAS 和 ACL 要相互一致；凭据放在目标已有配置机制中。
- Windows 原文通过删同级 tmp 排错；实际目录可能含 broker 数据，须先识别用途，不能默认删除。
- Flume 原文是文件日志 → exec source → memory channel → Kafka sink，依赖 Windows 上可用的 tail 工具。确认路径、channel 容量、topic、broker 和持久化要求，再适配配置。
- Qt / C++ 的 Kafka 客户端属于 librdkafka 编译任务，见[依赖编译](build.md)。

## JDK / Tomcat

原文覆盖 JDK 8、Tomcat 8.5、Ubuntu / CentOS / Jetson 和 systemd。根据应用要求选 JDK，ARM 与 x86 的 `JAVA_HOME` 不同；避免复制固定内存参数。

Tomcat 启动脚本会派生进程时，应配置相符的服务类型、PID 和停止方式。应用外置数据与 WAR 产物分开管理。Java 运行正常不代表应用连接数据库或媒体服务正常；验证深度由当前任务决定。
