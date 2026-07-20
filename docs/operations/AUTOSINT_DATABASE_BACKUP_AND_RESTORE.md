# AUTOSINT Database Backup And Restore

- Status: Current synthetic test contract
- Authority: Canonical local-development backup and restore runbook
- Version: 2.1
- Owner: AUTOSINT Data Platform
- Last reviewed: 2026-07-20
- Supersedes: Unspecified or repository-persisted local backup tests
- Superseded by: None
- Runtime truth: Bounded; the isolated synthetic backup/restore acceptance passed, but no production backup or restore is claimed
- Scope: Isolated local development/test PostgreSQL only
- Production backup/restore: Not authorized by this workflow

## Synthetic Backup Test

Preview:

```bash
.venv/bin/python scripts/manage_autosint_postgres.py --backup-test --json
```

Execute only after approval:

```bash
.venv/bin/python scripts/manage_autosint_postgres.py --backup-test --execute --json
```

The manager creates a unique database named
`autosint_backup_<random-hex>`, applies canonical migrations, inserts one
synthetic marker, and runs `pg_dump --format=custom`. The dump remains in
memory and is not written into the repository or an artifact directory. The
manager drops only the generated synthetic database during cleanup.

The backup receipt verifies the custom dump magic, migration revision, public
schema inventory hash, required extension versions, row-count hash, and
synthetic content hash. It does not expose dump bytes or database contents.

## Synthetic Restore And Integrity Test

Preview and execute use `--restore-test` in the same way. The executed test:

1. creates a unique synthetic source database;
2. applies migrations and inserts the synthetic marker;
3. creates an in-memory custom-format dump;
4. creates a second unique `autosint_restore_<random-hex>` database;
5. restores the dump into that database;
6. compares source and restored migration revision, public/legacy table
   inventory, extension versions, per-table row counts, and synthetic content
   hash;
7. drops only those two generated databases.

It never dumps, restores, truncates, or drops the normal `idos` local
development database. Database names are validated against a fixed synthetic
name pattern before `createdb` or `dropdb` is invoked.

## Boundaries

- No real Evidence bodies or production data may be inserted into fixtures.
- No backup file containing real data may be committed or placed in a handoff.
- The manager never accepts an arbitrary backup path or database name.
- A failed cleanup is an explicit test failure requiring operator review; it
  does not authorize broader deletion.
- Reset is not restore. Reset uses its own double-confirmed, label-checked
  command documented in `AUTOSINT_POSTGRES_LOCAL_DEVELOPMENT.md`.
- When unmanaged host PGDATA exists, backup and restore commands require both
  preservation arguments. Synthetic source/restore names and the labelled
  isolated container are the only permitted targets.

The 2026-07-20 isolated review returned `BACKUP_TEST_PASSED` and
`RESTORE_TEST_PASSED`, including `migration_at_head=true` and all integrity
comparisons true. This proves the synthetic local workflow only; production
backup policy, production recovery point, and production restore authority
remain unapproved.
