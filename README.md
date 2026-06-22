# Rift

**Source control beyond Git.**

Rift is an independent, permission-aware, agent-native source-control system.
It models changes, files, secrets, views, workspaces, reviews, and releases as
granular versioned objects instead of treating visibility as a repository-level
switch.

- Website: <https://riftvcs.dev>
- GitHub: <https://github.com/riftvcs/rift>
- CLI: `rift`
- Package namespace: `riftvcs`
- License: Apache-2.0

## Why Rift?

Rift is not a Git wrapper and is not Git-based internally. Git import/export may
exist later for migration and interoperability, but the core model is its own
object store, change graph, permission layer, and workspace layer.

The metaphor fits the product: Rift creates controlled separations in one source
graph, including public/private views, embargoed changes, agent workspaces, and
team-specific visibility, without forcing projects into separate repositories.

The CLI should stay short and direct:

```bash
rift init
rift status
rift record
rift view create public
rift secret add env.prod
rift workspace create --agent
```

## Core primitives

- content-addressed object store
- change graph
- permissioned views
- secret objects
- snapshots
- workspaces
- review/release policies
- native CLI and daemon/server protocol

## Current project structure

```text
rift/
  README.md
  LICENSE
  docs/
    research-spec.md
    architecture.md
  site/
    index.html
    research-pages.css
  src/
    README.md
```

## First implementation spike

The first prototype should be local-only and must not use Git as storage:

1. `rift init` creates `.rift/`.
2. `.rift/objects/` stores content-addressed blobs.
3. `.rift/db.sqlite` stores paths, snapshots and changes.
4. `rift record -m "message"` records a snapshot/change.
5. `rift status` shows changed paths.
6. `rift log` shows the change graph.
7. Later: `rift view`, `rift secret`, `rift workspace`.

## Open source

Rift is built in public under the Apache License 2.0. Contributions submitted
to this repository are licensed under Apache-2.0 unless explicitly stated
otherwise.
