# Prisma CLI CN

**中文找命令，保留 Prisma 7 原始参考。**

基于 [prisma/skills 的 prisma-cli](https://github.com/prisma/skills/tree/main/prisma-cli) 小幅适配，独立维护、非官方。适用于已有 **Prisma ORM 7** 项目；上游参考版本为 **7.9.1**，不是通用最新版指南。

## 保留与补充

保留初始化、客户端生成、开发数据库、迁移、数据库操作和诊断命令的原流程，以及全部 20 个参考文件。保留上游对 ORM、Platform/Compute 和破坏性命令的区分。

中文补充按“反向生成模型、同步开发库、开发迁移、部署迁移、检查差异、生成客户端”找到对应参考，解释操作对象与实际结果，避免把生成、比较和应用混为一谈。

## 安装与调用

```bash
npx skills add batespaige357-tech/prisma-cli-cn --skill prisma-cli-cn
```

对助手说：“用 prisma-cli-cn 帮我找到这个 Prisma 7 任务对应的命令，先说明它会改什么。”Codex 可使用 `$prisma-cli-cn`。手动安装时复制 `skills/prisma-cli-cn` 完整目录，保留 references。

本包提供工作流和参考文档，不包含 Prisma CLI、数据库或连接凭据。命令使用项目已有的匹配版本。Prisma 8、连接修复和新项目选型请使用[上游 prisma-orm-setup](https://github.com/prisma/skills/tree/main/prisma-orm-setup)；Platform/Compute 需使用对应上游技能，本包不捆绑它们。

## 来源与验证

MIT，保留 Prisma 原版权与许可证，详见 [CHANGES.md](CHANGES.md)。metadata.author/version 保留的是上游信息。

已检查正文保留情况、20 个参考文件（清理三处行尾空格）、UTF-8、本地链接及技能格式。未连接数据库、执行 Prisma 命令或验证真实迁移；未进行助手行为评估。未运行前端编译，不含示例网页、效果截图或前后对比。
