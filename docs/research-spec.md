# Rift Product Research

Rift is an independent source-control system for repositories that need
granular visibility, secret-aware workflows, and isolated workspaces for humans
and agents.

## Product Thesis

Git is excellent at distributed versioning, but its permission and workspace
model is repository-centered. Modern teams often need finer boundaries:

- public and private changes in the same project graph
- embargoed security fixes
- versioned secrets with scoped materialization
- contractor, team, and agent-specific views
- disposable workspaces created from precise snapshots
- review and release policies attached to changes, not only branches

Rift should model those concerns as native source-control primitives instead of
treating them as external tooling conventions.

## Non-Goals

Rift is not a Git wrapper, a Git UI, or a hosting product. Git import/export can
exist for migration and interoperability, but Git must not define the internal
storage or permission model.

Rift is also not only a secret manager or an agent sandbox. Those capabilities
matter because they belong inside a broader source graph.

## Core Concepts

| Concept | Meaning |
| --- | --- |
| Repository | Container for a source graph and its policies |
| Object | Versioned content such as blobs, trees, generated artifacts, or secrets |
| Change | Reviewable unit of source evolution |
| Snapshot | Materialized state for a workspace or view |
| View | Permissioned projection of the source graph |
| Policy | Rules for visibility, review, release, audit, and secret access |
| Workspace | Local, remote, or in-memory working environment |

## Initial Prototype

The first implementation should prove that Rift can store and inspect source
history without using Git as its storage layer.

Minimum local commands:

- `rift init`
- `rift status`
- `rift record`
- `rift log`

Minimum local storage:

- `.rift/config.toml`
- `.rift/objects/`
- `.rift/db.sqlite`

The first prototype does not need network sync, hosting, review UI, or secret
materialization. Those features should build on the native object store and
change graph after the local model is solid.

## Differentiation

Existing tools provide useful lessons:

- Jujutsu improves change and history UX while remaining Git-compatible.
- Sapling demonstrates large-repository workflows and scalable graph UX.
- Pijul explores patch-oriented version control.
- git-crypt shows that encrypted content can live in a repository.
- Scalar and sparse checkout improve performance for large Git repositories.

Rift's distinct direction is a permissioned source graph where views, secrets,
policies, and agent workspaces are first-class concepts.

## Open Questions

- What is the smallest useful local object model?
- How should view-specific graph projections be addressed and verified?
- Which secret metadata belongs in the source graph, and which material must
  remain external?
- How should review, release, and audit policies compose across views?
- What compatibility bridge is enough for migration from Git-based projects?
