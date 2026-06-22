# Rift architecture notes

Rift must be designed as an independent source-control system, not as Git with extra metadata.

## Minimal local repository format

```text
.rift/
  config.toml
  db.sqlite
  objects/
    ab/
      abcdef...blob
  refs/
  keys/
  tmp/
```

## Core primitives

| Primitive | Purpose |
|---|---|
| Blob | content-addressed file content |
| Tree | directory snapshot |
| Change | semantic change object with parents, message, author, policy |
| View | permissioned projection over the graph |
| Secret | encrypted typed object, not plain file by default |
| Workspace | materialized working state for human or agent |
| Policy | rules for visibility, materialization, review and release |

## First storage decision

For the first spike:

- Use BLAKE3 or SHA-256 for object IDs.
- Store object files by hash under `.rift/objects/`.
- Store metadata in SQLite.
- Avoid Git packfiles, Git object format and Git refs.

## Possible command vocabulary

Avoid copying Git too literally where better words exist:

| Git-ish idea | Rift command candidate |
|---|---|
| commit | `record` |
| branch | `view` or `line` |
| checkout | `open` / `workspace` |
| stash | unnecessary if snapshots are first-class |
| remote | `peer` |
| pull/push | `sync` |
| log | `log` still fine |
| status | `status` still fine |

## First spike scope

```bash
rift init
rift status
rift record -m "initial import"
rift log
```

Everything else waits until the local object model is proven.
