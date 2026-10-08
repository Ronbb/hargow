# Hargow

**每日一啖，粤讲粤好。**

粤语产品，目标语言 `yue-Hant-HK`。与 Brioche 共用账号，学习数据按产品隔离。

已部署正式学习服务：首课「走进茶楼，先打个招呼」包含粤语对话、粤拼、词汇与语法、三种练习和预生成录音。与 Brioche 共用账号，学习、收藏、复习和设置按产品隔离。管理员从个人页进入。

产品仅拥有品牌配置、原创 SVG、固定 Chef 子模块与 Compose 装配。页面渲染和 HTTP 实现在 Chef，产品不复制业务。

```sh
git submodule update --init --recursive
docker compose --env-file <private-runtime.env> up --detach --wait
```

`compose.yaml` 仅引用 Chef 的共享部署模板，身份、学习、Web 与内部 Traefik 使用固定镜像。容器通过共享网关网络接入 HTTPS，不发布宿主端口；数据库连接、域名与密钥保存在本机私有配置。旧 `compose.launch.yaml` 仅保留历史准备页。

架构和完整验收范围见 [架构说明](docs/architecture.md)。秘密、账号与私有声音不提交。

## 正式 Web 构建

Web 学习入口已从固定 Chef 子模块直接构建；`apps/web` 仅包含 Hargow 品牌、产品配置、素材与构建入口。开发服务监听所有接口，端口 5174。

```sh
pnpm install --frozen-lockfile
pnpm typecheck
pnpm build
pnpm dev:web
```

`infra/Dockerfile.web` 构建正式 Web 镜像。生产装配和验证记录见 [部署记录](docs/production-20261008.md)。
