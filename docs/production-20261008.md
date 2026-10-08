# Hargow 首次正式部署

2026-10-08 已用 Docker Compose 启动独立身份、学习 API、Web 与内部 Traefik 四个服务，外部 HTTPS 网关从准备页切换到正式产品路由。无宿主 HTTP 端口。共享部署模板由 Chef 维护，产品只引用模板并提供私有配置。

两产品共用原 PostgreSQL 与媒体卷；身份迁到 `chef_identity`，学习和内容保留 `public`。运行使用独立非所有者 identity/learning/content 数据库登录；作者和迁移凭据不进入 Web 服务。原两账号、Brioche 所有课源/公开投影及发布状态在迁移前后逐项指纹核对一致；原 48 课目录保持。

Hargow 发布 `hargow-teahouse-pilot`，首课 `starter-teahouse-arrive` revision 3。课程与原创头像、六份实际 Qwen 粤语 WAV、32 个模型时间轴 cue 来自 hargow-courses。发布记录使用所有者直接授权，没有伪造人工审听或浏览器会话。

生产前完整备份并恢复验证 1,496 媒体对象；恢复副本实际验证共用账号、产品权限/课程/收藏/复习隔离、原生学习写入、六份录音哈希和 Range。切换时另保存最终冻结数据库快照并验证归档目录。生产库不包含演练账号。

线上目录、课程 SSR、两个 Brioche 入口与健康检查通过。390px/678px 实际浏览器无横向溢出，粤拼和词汇底部卡片正常。真实 iPhone、屏幕阅读器及真人语音质量验收仍需补充。

本次服务镜像构建自 Chef `2a67b9b`；Web 构建自 `91410c4`（之后仅服务装配与测试修改）。后续固定子模块含 CI 修复。镜像、所有者连接、私有角色配置、备份和网关旧配置只保存在本机，不提交凭据。生产 Compose 项目名显式为 `chef-hargow` / `chef-brioche`，避免与旧 `brioche` 项目混用；禁止使用旧 combined Compose 重启迁移后的应用。
