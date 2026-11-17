---
name: prisma-cli-cn
description: 中文 Prisma 7 命令路由与说明。Prisma ORM 7 CLI reference for existing Prisma 7 applications or explicitly selected Prisma 7 workflows. Covers prisma init, generate, migrate, db, dev, studio, and mcp. For setup, connection repair, or Prisma 8, use prisma-orm-setup; not the Prisma Platform CLI.
license: MIT
metadata:
  author: prisma
  version: "7.9.1"
---

# Prisma ORM 7 CLI reference

These commands and examples apply to **Prisma ORM 7** only. For setup, connection repair, or a Prisma 8 application, load [prisma-orm-setup](https://github.com/prisma/skills/tree/main/prisma-orm-setup).

Use the project's version-matched CLI. Do not install a floating `prisma@latest` to run these commands.

## Boundary: Platform and Compute

Do not confuse the stable ORM command (`prisma`) with the public-beta Platform package (`@prisma/cli`, binary `prisma-cli`). Use `prisma-compute` for Compute apps and workspace auth, and `prisma-postgres-setup` for Platform projects and databases.

## When to Apply

Reference this skill when:
- Setting up an explicitly selected Prisma 7 project (`prisma init`)
- Generating Prisma Client (`prisma generate`)
- Running database migrations (`prisma migrate`)
- Managing database state (`prisma db push/pull`)
- Using local development database (`prisma dev`)
- Debugging Prisma issues (`prisma debug`)
- Generating shell completions (`prisma complete`)

## Rule Categories by Priority

| Priority | Category | Impact | Prefix |
|----------|----------|--------|--------|
| 1 | Setup | HIGH | `init` |
| 2 | Generation | HIGH | `generate` |
| 3 | Development | HIGH | `dev` |
| 4 | Database | HIGH | `db-` |
| 5 | Migrations | CRITICAL | `migrate-` |
| 6 | Utility | MEDIUM | `complete`, `studio`, `validate`, `format`, `debug`, `mcp` |

## Command Categories

| Category | Commands | Purpose |
|----------|----------|---------|
| Setup | `init` | Initialize a Prisma project |
| Generation | `generate` | Generate Prisma Client |
| Validation | `validate`, `format` | Schema validation and formatting |
| Development | `dev` | Local Prisma Postgres for development |
| Database | `db pull`, `db push`, `db seed`, `db execute` | Direct database operations |
| Migrations | `migrate dev`, `migrate deploy`, `migrate reset`, `migrate status`, `migrate diff`, `migrate resolve` | Schema migrations |
| Utility | `complete`, `studio`, `mcp`, `version`, `debug` | Shell, development, and AI tooling |

## Quick Reference

### Project Setup

```bash
# Initialize new project (creates prisma/ folder and prisma.config.ts)
prisma init

# Initialize with specific database
prisma init --datasource-provider postgresql
prisma init --datasource-provider mysql
prisma init --datasource-provider sqlite

# Initialize with Prisma Postgres (cloud)
prisma init --db

# Initialize with an example model
prisma init --with-model

```

### Client Generation

```bash
# Generate Prisma Client
prisma generate

# Watch mode for development
prisma generate --watch

# Generate specific generator only
prisma generate --generator client
```

### Bun Runtime

When using Bun, always add the `--bun` flag so Prisma runs with the Bun runtime (otherwise it falls back to Node.js because of the CLI shebang):

```bash
bunx --bun prisma init
bunx --bun prisma generate
```

### Local Development Database

```bash
# Start local Prisma Postgres
prisma dev

# Start with specific name
prisma dev --name myproject

# Start in background (detached)
prisma dev --detach

# List all local instances
prisma dev ls

# Stop instance
prisma dev stop myproject

# Remove instance data
prisma dev rm myproject
```

### Database Operations

```bash
# Pull schema from existing database
prisma db pull

# Push schema to database (no migrations)
prisma db push

# Seed database
prisma db seed

# Execute raw SQL
prisma db execute --file ./script.sql
```

### Migrations (Development)

```bash
# Create and apply migration
prisma migrate dev

# Create migration with name
prisma migrate dev --name add_users_table

# Create migration without applying
prisma migrate dev --create-only

# Reset database and apply all migrations
prisma migrate reset
```

### Migrations (Production)

```bash
# Apply pending migrations (CI/CD)
prisma migrate deploy

# Check migration status
prisma migrate status

# Compare schemas and generate diff
prisma migrate diff --from-config-datasource --to-schema schema.prisma --script
```

### Utility Commands

```bash
# Open Prisma Studio (database GUI)
prisma studio

# Start Prisma's MCP server for AI tools
prisma mcp

# Show version info
prisma version
prisma -v

# Debug information
prisma debug

# Validate schema
prisma validate

# Format schema
prisma format

# Generate shell completion code
prisma complete zsh
```

## AI Safety Checkpoint

Prisma blocks destructive commands when it detects an AI agent until the agent has obtained explicit user consent. This covers `migrate reset`, `db push --force-reset`, and `db push --accept-data-loss`.

- Explain the exact data-loss impact and ask for consent immediately before running the command.
- Do not infer consent from earlier or unrelated messages.
- If automation needs the consent variable, set `PRISMA_USER_CONSENT_FOR_DANGEROUS_AI_ACTION` to the user's exact consent message. Do not invent the text.
- The Prisma MCP server deliberately has no `migrate-reset` tool.

Read `references/agent-safety.md` before any destructive Prisma command.

## Current Prisma CLI Setup

### New Configuration File

Use `prisma.config.ts` for CLI configuration:

```typescript
import 'dotenv/config'
import { defineConfig, env } from 'prisma/config'

export default defineConfig({
  schema: 'prisma/schema.prisma',
  migrations: {
    path: 'prisma/migrations',
    seed: 'tsx prisma/seed.ts',
  },
  datasource: {
    url: env('DATABASE_URL'),
  },
})
```

### Current Command Behavior

- Run `prisma generate` explicitly after `migrate dev`, `db push`, or other schema syncs when you need fresh client output
- Run `prisma db seed` explicitly after `migrate dev` or `migrate reset` when you need seed data
- Use `prisma db execute --file ...` for raw SQL scripts

### Environment Variables

Load environment variables explicitly in `prisma.config.ts`, commonly with `dotenv`:

```typescript
// prisma.config.ts
import 'dotenv/config'
```

## Rule Files

See individual rule files for detailed command documentation:

```
references/init.md           - Project initialization
references/generate.md       - Client generation
references/dev.md            - Local development database
references/db-pull.md        - Database introspection
references/db-push.md        - Schema push
references/db-seed.md        - Database seeding
references/db-execute.md     - Raw SQL execution
references/migrate-dev.md    - Development migrations
references/migrate-deploy.md - Production migrations
references/migrate-reset.md  - Database reset
references/migrate-status.md - Migration status
references/migrate-resolve.md - Migration resolution
references/migrate-diff.md   - Schema diffing
references/studio.md         - Database GUI
references/mcp.md            - Prisma MCP server
references/complete.md       - Shell completion generation
references/agent-safety.md   - AI consent checkpoint for destructive commands
references/validate.md       - Schema validation
references/format.md         - Schema formatting
references/debug.md          - Debug info
```

## How to Use

Use the command categories above for navigation, then open the specific command reference file you need.


## 中文适配 — prisma-cli-cn 新增

独立非官方适配，保留上游 Prisma ORM 7 的命令说明、版本边界及破坏性命令检查。metadata 中 author/version 沿用上游来源与参考版本，不代表本适配获得官方认证。

### 按中文意图选择参考

| 用户意图 | 先读的参考 | 必须分清 |
|---|---|---|
| 从已有数据库反向生成模型 | [db-pull.md](references/db-pull.md) | 更新本地 schema，不能当成向数据库部署 |
| 把模型同步到开发数据库 | [db-push.md](references/db-push.md) | 不生成迁移历史，不能与生产迁移混用 |
| 开发并生成迁移记录 | [migrate-dev.md](references/migrate-dev.md) | 面向开发，不能代替生产部署 |
| 部署已有迁移 | [migrate-deploy.md](references/migrate-deploy.md) | 使用已有迁移，不替用户编写新迁移 |
| 检查迁移状态或差异 | [migrate-status.md](references/migrate-status.md)、[migrate-diff.md](references/migrate-diff.md) | 查看或生成 SQL 不等于已经应用 |
| 重新生成客户端 | [generate.md](references/generate.md) | 生成客户端不等于同步数据库 |

### 版本和输出说明

先从项目依赖、锁文件和配置确认正在使用 Prisma ORM 7；不为了套用参考将项目升级或安装浮动最新版。Prisma 8、新项目选型、连接修复转向上游 prisma-orm-setup，本包没有包含该技能。Platform/Compute 仍遵守原边界。

用中文说明命令会读取、生成或修改什么，保留命令、参数、路径和错误码原样。只建议命令时明确尚未运行；运行后区分实际输出与推断，不能把生成成功写成迁移成功。分享诊断信息时隐藏连接字符串中的凭据。

命令应符合当前任务范围；遇到需要重置或接受数据丢失的操作，继续遵守原 [agent-safety.md](references/agent-safety.md)，不自动添加危险参数、不编造同意文本。本中文说明不改变原命令行为或提供数据库凭据。
