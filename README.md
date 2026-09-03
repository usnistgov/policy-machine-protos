# Policy Machine Protos

This repository contains the Protocol Buffer definitions for the NIST Policy Machine.

Protocol buffers are Google’s language-neutral, platform-neutral, extensible mechanism for serializing structured data. Learn more in the [Protocol Buffers documentation](https://developers.google.com/protocol-buffers).

The generated Java code from these definitions can be found in the [policy-machine-core](https://github.com/usnistgov/policy-machine-core) repository.


## Current Release Status

This project is actively maintained and considered stable. No new major version is currently planned. Feedback and contributions are welcome via issues and pull requests.

## APIs

All definitions live under `v1/`, using package `gov.nist.ngac.pm.proto.v1.*`:

- `model.proto` — core NGAC data model (nodes, etc.) shared by the other files.
- `pdp_query.proto` — `PolicyQueryService`, for querying an NGAC policy.
- `pdp_adjudication.proto` — `AdminAdjudicationService` (administrative operations, routines, and PML execution) and `ResourceAdjudicationService` (resource operations).
- `epp.proto` — `EPPService`, for processing event contexts.

## Usage

Compile the protos with `protoc` (or [`buf`](https://buf.build)), pointing the include path at the repository root so imports like `import "v1/model.proto";` resolve. For example, to generate Java sources:

```sh
protoc -I. --java_out=out v1/*.proto
```
## Versioning

Definitions are namespaced by major version directory (`v1/`). Backwards-incompatible changes should be introduced in a new version directory (e.g. `v2/`) rather than modifying `v1` in place, so existing consumers are not broken.
