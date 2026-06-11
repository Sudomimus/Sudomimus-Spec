# Sudomimus API specs

This repository holds the authoritative OpenAPI 3.1 contracts for the public
Sudomimus APIs. One file per public service.

| File | Service | Purpose |
| --- | --- | --- |
| [`connect.yaml`](connect.yaml) | `connect` | Token exchange + session revocation (Establish / StatusPoll / Redeem / Refresh / Info / Introspect / Logout / RevokeAll) |
| [`native.yaml`](native.yaml) | `native` | Direct-issue (Steam ticket / access key) + errand status polling (`GET /errand/{errandKey}/status`) |

## Source of truth

These specs are **hand-maintained here** and describe the surface that the
open-source SDKs are guaranteed to support. The platform's internal
implementation lives in the private `sudomimus/sudomimus-core-monorepo` and is
**not** automatically synchronized with these files. When a spec change
requires a corresponding implementation change (or vice versa), link the
related core-monorepo PR in your description.

## Versioning

Spec changes follow SemVer on the `info.version` field of each document:

- **major** — backwards-incompatible changes (removed endpoints, renamed fields, narrower types).
- **minor** — additive changes (new endpoints, new optional fields, broader types).
- **patch** — descriptive-only changes (docs, examples, summaries).

## Consumed by

This repository is consumed as a git submodule by both
`sudomimus/sudomimus` and `sudomimus/sudomimus-core-monorepo`, mounted at
`specs/` in each. In the `sudomimus` SDK repo, each package generates strongly
typed request / response / error models from its corresponding spec:

- `sdks/typescript/packages/connect` ← `specs/connect.yaml`
- `sdks/typescript/packages/native`  ← `specs/native.yaml`
- `sdks/python/packages/sudomimus-connect` ← `specs/connect.yaml`
- `sdks/python/packages/sudomimus-native`  ← `specs/native.yaml`

When you edit a spec file, regenerate the consumers in the consuming repo in the
same change. CI in this repository lints the specs; CI in the consuming repos
runs the generators and fails on any uncommitted drift.
