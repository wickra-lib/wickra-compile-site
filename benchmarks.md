---
title: Benchmarks
description: "Criterion micro-benchmarks for the codegen hot paths, in crates/compile-bench. Reproduce with."
---

# Benchmarks

::: tip Looking for the indicator library's numbers?
This page is about Wickra Compile. Wickra's own indicator benchmarks — the
comparison against TA-Lib, talipp, pandas-ta and the other Rust TA crates —
live at [wickra.org](https://wickra.org/benchmarks).
:::

Criterion micro-benchmarks for the codegen hot paths, in `crates/compile-bench`.
Reproduce with:

```bash
cargo bench -p compile-bench
```

The figures below are indicative single-machine numbers (developer laptop, Rust
release build); treat them as orders of magnitude, not a spec. The nightly
`bench.yml` workflow re-runs the suite and uploads the report.

| Operation | What it measures | Time |
|-----------|------------------|------|
| `spec_hash` | Canonical serialisation + SHA-256 of a `StrategySpec`. | ~13 µs |
| `project_hash` | Hashing the generated file set in path order. | ~10 µs |
| `generate` (wasm) | Full codegen: validate → render → manifest, no `cargo`. | ~43 µs |
| `generate` (binary) | Same, targeting a native binary. | ~42 µs |
| `generate` (no_std) | Same, targeting a `no_std` MCU. | ~47 µs |
| `manifest_of` | Manifest for a spec without materialising files. | ~46 µs |

Code generation is cheap — tens of microseconds — because it is pure data
templating and hashing with no compilation. The optional `cargo build` step
dominates end-to-end time by orders of magnitude and is deliberately **not**
part of these microbenchmarks; it depends on the target toolchain and is
measured separately.

The numbers above are the ones in the repository's [`BENCHMARKS.md`](https://github.com/wickra-lib/wickra-compile/blob/main/BENCHMARKS.md), measured with the commands it names.
