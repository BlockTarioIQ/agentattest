# Modifications (Apache-2.0 §4(b))

This branch (`rhesia/wrapper`) is maintained by Rhesia contributors on top of upstream agentattest. It is additive: **no upstream file is changed**. Upstream copyright and license (`LICENSE`) are unchanged. This work does not imply endorsement by the upstream authors.

| File | Change | Why |
|---|---|---|
| `contracts_embed.go` | Added (root package `agentattest`) | Embeds the contract pack (`schemas/`, `policies/default.rego`, `tests/golden/context.schema.json`) byte-for-byte so the verifier works without a checkout on disk |
| `pkg/agentattest/agentattest.go` | Added | Thin exported wrapper over `internal/verify`, `internal/predicate`, `internal/gitbind`, `internal/signing` so other modules can use agentattest as a library. Adds `BindRange` (CI binding of a committed `base..head` change); everything else delegates |
| `pkg/agentattest/agentattest_test.go` | Added | All upstream golden fixtures through the wrapper; embedded-pack drift check; range-binding round trip |
| `MODIFICATIONS.md` | Added | This record |

Base commit: `fabfab962b68a06828ea8608d23da36e4b3ddcce` (tag `v0.1.0`).

Sync procedure: fast-forward `main` to upstream, rebase `rhesia/wrapper` onto the new upstream tag, run `go test ./...` (upstream suite, including the boundary test, plus the wrapper tests), then bump the pin in Rhesia (see Rhesia ADR-0005).

The wrapper is offered upstream as an additive contribution.
