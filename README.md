# Fluxer messaging platform

A multi-service messaging application with web and desktop clients, API services, message delivery and media processing.

## Architecture and stack

`fluxer_app` is the web client; `fluxer_desktop` wraps desktop delivery; `fluxer_api` owns the API; Rust services such as `fluxer_messages`, `fluxer_users`, `fluxer_media_proxy` and `fluxer_push` split backend responsibilities. `tools/dev` orchestrates local services and infrastructure.

## Requirements

Node/pnpm from the root manifest, Rust/Cargo with edition 2024 support, and the infrastructure expected by the development tool. The workspace spans both JavaScript and Rust dependency graphs.

## Installation and local development

The root manifest routes development through its Rust orchestrator:

```sh
pnpm install --frozen-lockfile
pnpm dev:bootstrap
pnpm dev
```

Bootstrap can install/start infrastructure. Inspect `tools/dev` and `config/` before running it on a shared host.

## Configuration

Service configuration lives in `config/` and shared configuration packages. Keep environment-specific credentials outside source. Use separate public and internal service addresses; do not expose storage or management services directly.

## Testing

`pnpm lint` runs Biome, ESLint and generated-data/config checks. Rust package tests use `cargo test -p <crate-name>` from the workspace. The root has no generic `test` npm script; use the relevant package manifest or CI step.

## Deployment and integrations

Review `deploy/` and `fluxer_docs/` for deployment assets. `pnpm build` runs the Rust development tool build pipeline; a complete deployment needs coordinated configuration for API, gateway, media, databases and clients.

## Source provenance and license

This repository imports source from [fluxerapp/fluxer](https://github.com/fluxerapp/fluxer). Original product functionality belongs to its upstream contributors. The local history begins with a November 2026 source snapshot; it does not retain upstream development history or prove the exact upstream revision. GitHub reports the upstream repository was created on 2026-01-01; that is repository-origin evidence, not the date of this contribution. Existing year folders are retained as local organization.

Preserve `LICENSE` and existing third-party notices when redistributing. Missing root license text was recovered from the upstream repository during this maintenance pass; existing license files were preserved.

## Validation status

Setup and test commands above were checked against this checkout’s manifests, scripts and entry points. Full dependency installation, application builds and integration tests were not performed in this maintenance pass. The Node/Rust workspace dependencies and multi-service infrastructure were not provisioned. These instructions identify the supported workflow without claiming a successful product build.

See [source provenance](SOURCE_PROVENANCE.md) for pinned upstream license retrieval evidence and redistribution limitations.
