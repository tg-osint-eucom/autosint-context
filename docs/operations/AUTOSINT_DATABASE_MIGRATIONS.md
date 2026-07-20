# AUTOSINT Database Migrations

- Status: Current migration authority
- Authority: Canonical ordered PostgreSQL migration runbook
- Version: 2.1
- Owner: AUTOSINT Data Platform
- Last reviewed: 2026-07-20
- Supersedes: Opportunistic runtime DDL and parallel `idos` migration authority
- Superseded by: None
- Canonical framework: Alembic
- Canonical schema: `public`
- Version table: `public.alembic_version`
- Current tracked head: `20260719_0004`
- Runtime truth: BOUNDED — the tracked chain was applied to the isolated local development/test target; no production target is approved

## Authority

`alembic.ini` and `database/migrations/` are the only current ordered migration
authority for the root SQLAlchemy models. Runtime helpers must not create or
alter tables opportunistically. `core.autonomy_ledger.ensure_autonomy_ledger`
therefore verifies the migrated relation and fails with
`DATABASE_MIGRATIONS_REQUIRED` instead of executing DDL.

The old `src/idos_pipeline/jobs/apply_migrations.py` path is not a migration
authority. It references an absent schema file, expects a parallel `idos`
schema, and is fail-closed unless `AUTOSINT_ENABLE_LEGACY_IDOS_SCHEMA=1` is set
for a separately approved legacy migration task. That flag does not make the
legacy schema canonical.

## Configuration

Database URL precedence is:

1. explicit function/CLI argument;
2. `AUTOSINT_DATABASE_URL`;
3. `DATABASE_URL`;
4. passwordless local default at `127.0.0.1:55432`.

`AUTOSINT_DATABASE_SCHEMA` must be `public`. Any other value fails closed.

## Safe Application

Preview:

```bash
.venv/bin/python scripts/manage_autosint_postgres.py --migrate --json
```

Apply only after current service and volume identity are known:

```bash
.venv/bin/python scripts/manage_autosint_postgres.py --migrate --execute --json
```

When unmanaged host PGDATA is detected, append both exact preservation
arguments from `AUTOSINT_POSTGRES_LOCAL_DEVELOPMENT.md`. The migration then
targets only the labelled managed container and volume. It must never connect
to, stamp, inspect, or adopt the preserved candidate.

Before online migration, both the manager and Alembic inspect schema metadata,
not table contents. Migration stops with
`EXISTING_DATABASE_REQUIRES_OPERATOR_DECISION` when either condition holds:

- an unversioned `public` schema already contains application tables;
- the legacy `idos` schema contains tables.

The PostGIS-owned `public.spatial_ref_sys` table alone is not treated as user
data. No migration stamps or adopts an unknown existing database.

## Ordered Chain

Revision `20260719_0001` creates the current root ORM table set and the required
extensions:

- `pgcrypto`
- `postgis`
- `vector`

The forward-only V2.1 revisions then add isolated domains without changing
canonical Evidence, case, source, Thread, packet, OSIR, proof, apply/import, or
commander-ready state:

- `20260719_0002`: dedicated PIR advisory tables and audited status/review rows;
- `20260719_0003`: bounded Agent Runtime runs, tasks, append-only events,
  candidate results, and typed handoffs;
- `20260719_0004`: replay-first ScoutGenerationService task, event, and result
  persistence contracts.

Every revision is explicit and schema-qualified. Destructive downgrade is
disabled; corrections use an operator-reviewed forward migration. Never use a
downgrade, manual `DROP`, or `alembic stamp` to force an unknown database into
compliance.

Offline SQL can be rendered without connecting to PostgreSQL:

```bash
.venv/bin/python -m alembic -c alembic.ini upgrade head --sql
```

Offline SQL rendering does not prove extension availability, migration
application, database health, or release readiness.

The isolated V2.1 acceptance target retains database name `idos` and schema
`public` for compatibility. This is recorded as
`LEGACY_DATABASE_NAME_RETAINED_FOR_COMPATIBILITY`; it does not restore the
disabled legacy `idos` schema or make the local target production data. The
bounded acceptance proved revision `20260719_0004`, the expected public-table
inventory, and `pgcrypto`, `postgis`, and `vector` availability across a
stop/start reconnect.

## Release Gate

`scripts/validate_release_surface.sh` now requires both manager health and
schema smoke before it can emit `RELEASE_SURFACE_READY`. It does not load
`.env` by default. Loading `.env` requires the explicit
`AUTOSINT_LOAD_ENV_FILE=1` setting and is outside normal proof-first execution.

When the preservation exception is in force, the validator requires this exact
environment pair or fails before database access:

```bash
AUTOSINT_DATABASE_URL=postgresql+psycopg://idos@127.0.0.1:55432/idos
AUTOSINT_UNMANAGED_HOST_PGDATA_POLICY=preserve-and-use-isolated-managed
AUTOSINT_CONFIRM_PRESERVE_UNMANAGED_HOST_PGDATA=1
```

`AUTOSINT_DATABASE_URL` must separately identify the approved isolated
loopback target. These variables do not approve a production target.
