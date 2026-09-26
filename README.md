# SalesClaw Commerce

<p align="center">
  <img src="web/public/icons/logo-1024.png" alt="SalesClaw logo" width="112" />
</p>

<p align="center">
  <strong>面向国内多渠道零售的多数字员工平台</strong><br />
  基于 SalesClaw Agent 运行时，覆盖商品、营销、内容与直播、客服、订单、履约、售后和经营分析全链路。
</p>

<p align="center">
  <a href="https://github.com/Xx-173/salesclaw-commerce">GitHub</a> ·
  <a href="docs/API.md">API</a> ·
  <a href="docs/ACL-MATRIX.md">权限模型</a> ·
  <a href="SECURITY.md">安全策略</a>
</p>

## 产品定位

SalesClaw Commerce 是面向国内多渠道零售经营的数字员工平台。平台基于 SalesClaw 的 Agent 运行与治理能力，围绕商品、营销、内容与直播、客服、交易、履约、售后复购和经营分析组织业务工作流，并支持自研业务软件通过事件 API 接入。

当前版本提供门店隔离、业务事件接入与全链路经营视图。微信小程序、淘宝/天猫、知乎和百度连接器仍处于预留状态；接入真实业务 API、客户数据或外发动作前，必须完成授权、最小权限和审计配置。

## 核心能力

- Agent Profile、Workspace、Session、Memory、Skills、MCP 与 Subagent 的隔离管理。
- 基于 Pi Agent Runtime 的流式对话、工具调用、会话恢复和后台任务。
- 多用户认证、角色权限、Workspace ACL、操作审计与安全执行边界。
- Web、Electron Desktop 与可配置消息渠道入口。
- Cron、固定间隔和一次性自动化任务，以及运行历史与通知。
- Host / Docker 双执行模式，支持将 Agent 的能力范围与宿主环境分离。
- 国内零售全链路领域模型，支持按 Workspace 隔离店铺，并通过自研软件事件 API 记录商品、营销、内容/直播、客服、订单、履约、售后与经营分析活动。
- 第三方平台能力目录明确标记为预留状态；Agent 可继续通过 Workspace 级 MCP 配置连接经授权的业务 API。

## 本地启动

要求：Node.js 20+，并按需准备 Docker 与模型/渠道配置。

```bash
npm ci
npm run dev:all
```

浏览器访问本地服务后完成管理员初始化。真实 Provider、渠道和容器运行时均需要由部署者自行配置；请勿将 API Key、Cookie、Token 或客户数据提交到仓库。

常用校验：

```bash
npm run typecheck
npm test -- --run
npm run build:all
```

## 项目结构

```text
src/                    后端、认证、运行时、权限与渠道适配
web/                    Web / PWA 客户端
electron/               Desktop Shell
container/agent-runner/ 隔离的 Agent 运行环境
docs/                   API、安全、权限与运行说明
```

## 部署与安全

- 生产环境使用 HTTPS / WSS，并把密钥放在受管密钥存储或部署环境变量中。
- 将消息渠道、客户数据和外发能力绑定到最小权限的 Workspace 与角色。
- 对销售自动化场景，为频控、停用、人工接管、同意状态和审计留出明确控制点。
- 默认容器镜像为 `ghcr.io/xx-173/salesclaw-agent:latest`；首次使用前请发布或显式指定你自己的 `SALESCLAW_CONTAINER_IMAGE` / `CONTAINER_IMAGE`。

## 许可证

本仓库遵循 MIT License。`LICENSE` 中保留了随源码附带的版权与许可声明；对本项目的新增修改适用同一许可证。
