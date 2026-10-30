# moyai-lzcapp

[Moyai](https://github.com/BerriAI/moyai) 的 LazyCat LPK 打包 —— 自托管后台编码代理（LiteLLM 团队出品）。

## 形态

- 单容器镜像：`ghcr.io/berriai/moyai`，端口 8787，数据在 `/data`
- 镜像交付：**direct + digest 固定**（GHCR 只有 mutable `quickstart` tag，mirror 校验不可用，同 Nostos/Merran 模式）
- 版本策略：`channel: custom` + `sort: created` + `tag_regex: ^quickstart$` + `bump: patch`
  digest 变化才递增 patch，未变化则 no-op
- 仅喵喵商店；仅 PC 平台

## 部署参数（设置向导）

| 参数 | 类型 | 说明 |
|------|------|------|
| `workspace_password` | secret | 工作区管理员登录密码，自动生成 |
| `admin_user` | string | 管理员用户名（默认 admin） |
| `litellm_api_base` | string | LiteLLM 兼容模型网关地址 |
| `litellm_api_key` | secret | 网关 API 密钥 |
| `moyai_models` | string | 暴露给代理的默认模型列表（provider/model，逗号分隔） |

`ENCRYPTION_KEY` 用 `stable_secret` 生成并保持稳定 —— 改动会导致已存凭据不可解密。

## 登录

首启前 `WORKSPACE_PASSWORD` 已通过部署参数注入，登录用户名 `admin`。

## 持久化

`/lzcapp/var/data` → `/data`（工作区数据）
