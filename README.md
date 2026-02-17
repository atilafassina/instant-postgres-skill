# instant-postgres

Instant Postgres database provisioning via [Claimable Postgres by Neon](https://pg.new). No account required.

## What is this?

A toolkit for spinning up instant Postgres databases. Databases are available for 72 hours and can be claimed to a Neon account for permanent use.

## Features

- **Zero configuration** - Get a database with a single command
- **No account required** - Start immediately, claim later if you want to keep it
- **Multiple integration options** - CLI, SDK, Vite plugin, or REST API
- **Seed support** - Initialize your database with a SQL file

## Quick Start

```bash
npx get-db
```

Creates a database and writes `DATABASE_URL` to `.env`.

## Tools

### CLI (`get-db`)

```bash
npx get-db
```

**Options:**

- `-y, --yes` - Skip prompts, use defaults
- `-e, --env <path>` - Target env file (default: `./.env`)
- `-k, --key <name>` - Variable name (default: `DATABASE_URL`)
- `-s, --seed <path>` - SQL file to initialize the database
- `-L, --logical-replication` - Enable logical replication (for ElectricSQL/TanStack DB)

### SDK (`get-db/sdk`)

```typescript
import { instantPostgres } from "get-db/sdk";

const db = await instantPostgres();
console.log(db.connectionString);
```

### Vite Plugin (`vite-plugin-db`)

```bash
npm install vite-plugin-db --save-dev
```

```typescript
// vite.config.ts
import { defineConfig } from "vite";
import { postgres } from "vite-plugin-db";

export default defineConfig({
  plugins: [postgres()],
});
```

Automatically provisions a database when you run `vite dev`.

### REST API

For custom integrations or non-Node.js environments:

```bash
curl -X POST https://pg.new/api/v1/database \
  -H "Content-Type: application/json" \
  -d '{"ref": "my-app"}'
```

Returns:

```json
{
  "id": "...",
  "connection_string": "postgresql://...",
  "claim_url": "https://pg.new/claim/...",
  "expires_at": "..."
}
```

See [references/api.md](./references/api.md) for full API documentation.

## Database Specs

| Spec             | Value                     |
| ---------------- | ------------------------- |
| Postgres Version | 17                        |
| Region           | AWS us-east-2             |
| SSL              | Required                  |
| TTL              | 72 hours (unless claimed) |

## Claiming Your Database

Databases expire after 72 hours. To keep one permanently:

1. Find the claim URL in the CLI output or `.env` file (`PUBLIC_CLAIM_URL`)
2. Visit the URL to attach the database to your Neon account
3. Manage it from the [Neon Console](https://console.neon.tech)

## License

MIT
