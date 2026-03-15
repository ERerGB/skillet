# Skillet

面向自媒体创作者的内容生产力终端。

## Concept

创作者通过 IM Agent（WhatsApp / Telegram / 微信等）：

```
IM → 查找 Skill Hub → 读取 Skills → 内容组织编排 → 发布
```

Skillet 是**产品层**——编排 [SkillRank](https://github.com/ERerGB/skillrank)（Hub 发现与排名）、[Prism](https://github.com/ERerGB/prism)（知识图谱）和平台 SDK（发布），为创作者提供端到端的内容工作流。

## Architecture

| Dependency | Role |
|------------|------|
| **SkillRank** | Hub 排名引擎 — 发现最优质的 Skill Hub |
| **Prism** | 知识图谱 — 内容摄入、实体提取、语义检索 |
| **Platform SDKs** | 多平台发布适配器 |

## V1 MVP

完成流程中**任意一个完整环节**即可验证：
1. 通过 IM 发现并列出 Hub 中的 Skill
2. 加载一个 Skill 并执行其核心能力
3. 生成一篇符合平台规范的内容
4. 发布到任一平台

V1 目标平台（图文优先）：小红书 · 微信公众号 · X · Instagram · Threads

## Development

```bash
pnpm install
pnpm dev          # Local dev
pnpm test         # Run tests
pnpm gen:index    # Regenerate doc indexes
```

## Documentation

- [ADRs](doc/adr/) — Architectural decisions
- [AGENTS.md](AGENTS.md) — Mandatory rules for AI agents and developers

## License

MIT
