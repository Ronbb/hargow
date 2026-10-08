# Hargow

**每日一啖，粤讲粤好。**

粤语产品，目标语言 `yue-Hant-HK`。与 Brioche 共用账号，学习数据按产品隔离。

当前已部署独立 HTTPS 品牌入口，页面明确显示「课程准备中」。这不是可用的课程或登录服务：语言中立课程运行、粤语内容与录音、共用身份和产品学习 API 仍待贯通。入口不连接数据库、不转发 Brioche API。

产品仅拥有品牌配置、原创 SVG、固定 Chef 子模块与 Compose 装配。页面渲染和 HTTP 实现在 Chef，产品不复制业务。

```sh
git submodule update --init --recursive
docker compose -f compose.launch.yaml up --build --detach --wait
```

容器通过已有共享网关网络接入 HTTPS，不发布宿主端口；网关域名与证书保持本机配置。正式学习服务就绪后替换 launch 服务。

架构和完整验收范围见 [架构说明](docs/architecture.md)。秘密、账号与私有声音不提交。
