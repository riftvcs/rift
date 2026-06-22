# Rift Implementation

This directory is reserved for the first Rift implementation.

Rift is intended to become its own source-control system. Do not start by
wrapping Git or relying on Git as the core storage model.

First implementation milestone:

1. Choose implementation language.
   - Go is attractive for a portable CLI and daemon.
   - Rust is attractive for storage correctness and performance.
2. Implement local `.rift/` repository format.
3. Store blobs in `.rift/objects/` by hash.
4. Store metadata in SQLite.
5. Implement:
   - `rift init`
   - `rift status`
   - `rift record`
   - `rift log`
6. Only after local basics work, explore:
   - views
   - secret objects
   - workspaces
   - server protocol
   - Git import/export for migration only

No implementation has been started yet; this is a clean starting point.
