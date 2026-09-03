# Developer Setup

Instructions for setting up a local development environment for `policy-machine-protos`.

## Prerequisites

-   **[`protoc`](https://grpc.io/docs/protoc-installation/)** (the Protocol Buffer compiler), or [`buf`](https://buf.build)
-   **Git**

## Clone the repository

```
git clone https://github.com/usnistgov/policy-machine-protos.git
cd policy-machine-protos
```

## Layout

Definitions live under `v1/`, using package `gov.nist.ngac.pm.proto.v1.*`:

-   `model.proto` — core NGAC data model (nodes, etc.) shared by the other files.
-   `pdp_query.proto` — `PolicyQueryService`, for querying an NGAC policy.
-   `pdp_adjudication.proto` — `AdminAdjudicationService` and `ResourceAdjudicationService`.
-   `epp.proto` — `EPPService`, for processing event contexts.

## Build / compile

Compile with `protoc`, pointing the include path at the repository root so imports like `import "v1/model.proto";` resolve:

```
protoc -I. --java_out=out v1/*.proto
```

Substitute `--java_out` for whichever language plugin you need (`--go_out`, `--python_out`, etc.), or use `buf generate` with a `buf.gen.yaml` targeting the same output.

## Consuming these protos

The generated Java code from these definitions is published via [policy-machine-core](https://github.com/usnistgov/policy-machine-core), which pins this repository as a `grpc/protos` git submodule. If you're updating protos here for use downstream, bump that submodule's pinned commit in `policy-machine-core` once your change lands on `main`.