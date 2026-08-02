# Sudomimus API specs

This repository holds the authoritative OpenAPI 3.1 contracts for the public
Sudomimus APIs. One file per public service.

| File | Service | Purpose |
| --- | --- | --- |
| [`connect.yaml`](connect.yaml) | `connect` | Inquiry lifecycle (Establish / StatusPoll / Redeem / Info) |
| [`session.yaml`](session.yaml) | `session-api` | Ordinary application session lifecycle (Refresh / Introspect / Logout / RevokeAll) |
| [`native.yaml`](native.yaml) | `native` | Direct-issue (Steam ticket / access key) + errand status polling (`GET /errand/{errandKey}/status`) |
| [`device.yaml`](device.yaml) | `device-api` | Device authorization for public clients (`POST /device-authorize` / `POST /device-token`) |

## Public Contract

These specs define the public API surface that Sudomimus SDKs and integrating
applications can rely on. Keep descriptions focused on externally observable
behavior: endpoints, authentication requirements, request / response schemas,
error reasons, and compatibility notes.

## Versioning

Spec changes follow SemVer on the `info.version` field of each document:

- **major** — backwards-incompatible changes (removed endpoints, renamed fields, narrower types).
- **minor** — additive changes (new endpoints, new optional fields, broader types).
- **patch** — descriptive-only changes (docs, examples, summaries).

## Consumers

Public reference documentation and generated clients consume these contracts.
Client-generation repositories own their package mappings; this repository owns
only the OpenAPI source documents and their synchronization checks.
