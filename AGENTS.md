# AGENTS.md — SkillNet

## What is SkillNet

面向自媒体创作者的 **内容生产力终端**。

创作者通过 IM Agent 空间（WhatsApp / Telegram / 微信等）：
1. 通过 SkillRank 索引地址发现 Skill Hub
2. 从 Hub 中读取可用的 Skill（AI 能力模块）
3. 调用 Skill 完成内容组织、编排
4. 发布到目标平台

SkillNet 是产品层——组装 SkillRank（发现）+ Prism（图谱）+ 平台 SDK（发布），
向创作者提供端到端的内容工作流。

## Mandatory Rules

1. **ADR governance**: Every architectural decision in `doc/adr/`.
   ADRs are immutable once decided.
2. **Auto-generated indexes**: Never hand-edit between
   `<!-- INDEX:START -->` / `<!-- INDEX:END -->` markers.
3. **TDD**: Write failing tests first, then implement, then refactor.
4. **DRY**: Single authoritative representation for every piece of knowledge.
5. **Separation of concerns**: SkillNet does NOT re-implement ranking (SkillRank)
   or graph storage (Prism). It only orchestrates and presents.

## Architecture

```
创作者 (IM Agent)
    │
    ▼
┌─────────────────────────────────────────────────────┐
│  SkillNet（产品层）                                   │
│                                                     │
│  ┌──────────────┐  ┌───────────────┐  ┌──────────┐ │
│  │ Hub Discovery │  │ Skill Runner  │  │ Publisher │ │
│  │ (via SkillRank)│  │ (orchestrate) │  │ (平台SDK)│ │
│  └──────┬───────┘  └───────┬───────┘  └────┬─────┘ │
│         │                  │               │       │
└─────────┼──────────────────┼───────────────┼───────┘
          │                  │               │
          ▼                  ▼               ▼
    SkillRank API      Prism API       Platform APIs
    (Hub 排名)         (图谱/检索)     (小红书/公众号/X/IG/Threads)
```

## Dependencies

| Service | Role | Interface |
|---------|------|-----------|
| **SkillRank** | Hub 发现与排名 | HTTP API (`/rank`, `/hubs`, `/search`) |
| **Prism** | 内容图谱：摄入、提取、存储、检索 | HTTP API (`/mcp`) or local |
| **Platform SDKs** | 多平台发布 | 各平台原生 API |

## V1 Target Platforms

图文内容优先：
1. 小红书 (Xiaohongshu / RED)
2. 微信公众号 (WeChat Official Accounts)
3. Twitter / X
4. Instagram
5. Threads

## V1 MVP Scope

最小可行路径——完成以下任意一个环节即可验证：

```
IM → 查找 SkillHub → 读取 Skills → 内容组织编排 → 发布
                     ↑ 任意一步完成 = MVP ↑
```

## Reference Sub-Documents

| Document | Path | When to read |
|----------|------|--------------|
| Architecture details | `doc/agents/architecture.md` | Module design, data flow |
| Known issues | `doc/agents/known-issues.md` | Debugging, workarounds |
| DX Tooling | `doc/agents/dx-tooling.md` | Skills, commands, doc governance |

## Build & Dev

```bash
pnpm install
pnpm dev                        # Local dev
pnpm test                       # Run tests
npx tsx scripts/generate-doc-index.ts all  # Regenerate doc indexes
```
