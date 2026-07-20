# AUTOSINT PostgreSQL Local Development

- Status: Current foundation contract
- Authority: Canonical local PostgreSQL development and test runbook
- Version: 2.1
- Owner: AUTOSINT Data Platform
- Last reviewed: 2026-07-20
- Supersedes: Opportunistic local database startup and implicit schema creation
- Superseded by: None
- Runtime truth: No; use the manager's current status and health output
- Scope: One isolated local development/test PostgreSQL service only
- Canonical schema: `public`
- Endpoint: `127.0.0.1:55432`

## Safety Boundary

The manager checks only for the existence of conventional unmanaged Homebrew
PostgreSQL 16 data-directory candidates. It never enumerates or opens their
contents. If one exists, every runtime mutation fails closed by default with
`EXISTING_DATABASE_REQUIRES_OPERATOR_DECISION`, even though the target Docker
service and volume have separate names.

The only supported exception is an exact operator decision to preserve every
detected candidate untouched while using the separately named managed AUTOSINT
container and volume. Both of these arguments are required on every applicable
manager action:

```text
--unmanaged-host-pgdata-policy preserve-and-use-isolated-managed
--confirm-preserve-unmanaged-host-pgdata
```

The first argument alone is not authority, the confirmation alone is not
authority, and neither permits reading, connecting, migrating, moving,
renaming, deleting, re-permissioning, or reusing unmanaged PGDATA. The manager
records only bounded candidate metadata required to prove the preservation
boundary.

The tracked foundation never contains a password. The local container uses
PostgreSQL `trust` authentication and is safe only because Compose binds it to
`127.0.0.1`. Do not change the bind address to `0.0.0.0`, a LAN address, or a
remote interface.

The manager does not read `.env`, inspect PGDATA contents, pull images, build
images, install packages, or start a service unless the exact command is
explicitly requested. Mutating commands are dry-run by default and require
`--execute`.

The managed identities are fixed:

- project: `autosint-local-postgres-v21`
- container: `autosint-postgres-local-v21`
- volume: `autosint_pgdata_v21`
- image: `autosint/postgres-local:16-postgis3-pgvector0.8.0-v1`
- pinned base: `pgvector/pgvector:0.8.0-pg16-bookworm@sha256:a132765ec351c65111b5b675928a3a0515a466a40f97277329db8b8209ad8bc9`
- role: `idos`
- database: `idos` (`LEGACY_DATABASE_NAME_RETAINED_FOR_COMPATIBILITY`)
- schema: `public`

Both the container and volume must carry the V2.1 management labels. An
existing unlabeled or differently labeled target produces:

```text
EXISTING_DATABASE_REQUIRES_OPERATOR_DECISION
```

The manager does not inspect that volume's contents and does not modify it.

Every status/health receipt must expose the preservation and isolation fields
`unmanaged_host_pgdata_detected`, `unmanaged_host_pgdata_candidate_count`,
`unmanaged_host_pgdata_policy`, `unmanaged_host_pgdata_preserved`,
`unmanaged_host_pgdata_used`, `operator_confirmation_present`, and
`managed_target_isolated`. A successful exception requires preserved `true`,
used `false`, confirmation `true`, and isolated target `true`.

## Commands

Use the repository virtual environment:

```bash
.venv/bin/python scripts/manage_autosint_postgres.py --status --json
.venv/bin/python scripts/manage_autosint_postgres.py --health --json
.venv/bin/python scripts/manage_autosint_postgres.py --smoke --json
```

The default invocation is the same read-only status check:

```bash
.venv/bin/python scripts/manage_autosint_postgres.py
```

Preview mutations first:

```bash
.venv/bin/python scripts/manage_autosint_postgres.py --start --json
.venv/bin/python scripts/manage_autosint_postgres.py --migrate --json
.venv/bin/python scripts/manage_autosint_postgres.py --stop --json
```

After current operator approval, add `--execute` to the exact intended action
and include both unmanaged-PGDATA preservation arguments when a candidate is
present. `--start --execute` uses `--no-build`; it cannot silently pull or
build an image. If the pinned local image is absent, the result is
`BLOCKED_CONFIGURATION` with reason `PINNED_LOCAL_IMAGE_NOT_PRESENT`.

Building the image runs package installation inside the image and requires a
separate explicit network confirmation. The bounded build command is:

```bash
.venv/bin/python scripts/manage_autosint_postgres.py \
  --build-local-image \
  --confirm-build-network-access \
  --unmanaged-host-pgdata-policy preserve-and-use-isolated-managed \
  --confirm-preserve-unmanaged-host-pgdata \
  --execute --json
```

This may download packages into the pinned image only. It does not authorize
Docker installation, host package installation, a base-image pull outside the
tracked pinned build, or any unmanaged PGDATA access.

## Verified Local Development/Test Boundary

The 2026-07-20 pre-push review exercised the explicit preservation gate against
the isolated managed target. The manager kept the detected unmanaged candidate
unused and unchanged while the labelled container and volume were built,
started, migrated, health-checked, stopped, restarted, and reconnected on
`127.0.0.1:55432`. This is bounded local development/test evidence only. It is
not production-data approval, External Scout proof, pilot acceptance, or
authorization to reset any database.

## Status Classes

The manager uses the goal's explicit blocker vocabulary:

- `SERVICE_NOT_INSTALLED`
- `SERVICE_INSTALLED_NOT_RUNNING`
- `CONTAINER_RUNTIME_AVAILABLE_NO_SERVICE`
- `PORT_CONFLICT`
- `CONFIGURATION_MISMATCH`
- `MIGRATION_FAILURE`
- `AUTHENTICATION_FAILURE`
- `EXISTING_DATABASE_REQUIRES_OPERATOR_DECISION`
- `UNKNOWN`

`READY` means only that the managed local service is reachable, the migration
revision is at the tracked head, required extensions exist, and the requested
schema smoke passed. It is not External Scout runtime proof or release
readiness.

## Reset

Reset is restricted to the exactly named, correctly labeled managed volume.
It requires all three elements:

```bash
.venv/bin/python scripts/manage_autosint_postgres.py \
  --reset-local-dev-data \
  --confirm-destroy-isolated-local-dev-data \
  --unmanaged-host-pgdata-policy preserve-and-use-isolated-managed \
  --confirm-preserve-unmanaged-host-pgdata \
  --execute
```

Neither confirmation nor a matching name permits deletion of an unknown or
unlabeled volume. The manager never accepts a filesystem path or recursive
delete target.
