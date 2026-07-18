# About Wickra Compile

Wickra Compile turns a strategy spec into a standalone deployable — a WASM module,
a self-contained binary, or a `no_std` artifact for microcontrollers. A compile is
a JSON document — **data, not code** — so the manifest it produces is byte-for-byte
identical in every one of ten languages and reproducible across runs.

## What makes it different

- **Strategy in, deployable out.** You write your strategy as a `CompileSpec` — the
  same `StrategySpec` `wickra-backtest` runs — and the compiler generates a
  standalone Rust project that embeds it verbatim and calls the Wickra engine. No
  interpreter, no runtime spec parsing.
- **Three targets.** A WASM module, a self-contained native binary, or a `no_std`
  artifact for an allow-listed microcontroller — one spec, whichever target you name.
- **A reproducible manifest.** The list of generated files with their hashes plus the
  canonical spec hash (`project_hash`) is byte-identical across all ten bindings.
- **The Wickra engine, embedded.** The generated project calls the same core that
  powers a backtest, so a compiled strategy sees exactly the same numbers.

## Why it exists

Deploying a strategy usually means rewriting it in whatever language the target
runtime speaks. Wickra Compile makes the strategy **data** and generates the
deployable **once**, from a spec, exposing the compiler as a JSON-over-C-ABI data
API to Rust, Python, Node.js, WASM and — over a C ABI — C, C++, C#, Go, Java and R.
Write the spec anywhere, emit the same project everywhere.

## Open source

Released under the **MIT OR Apache-2.0** license — permissive, OSI-approved, free
for any use including commercial. Source, issues and releases on
[GitHub](https://github.com/wickra-lib/wickra-compile).

## Disclaimer

Wickra Compile is a software library, **not** a trading system, and is provided
**as-is with no warranty**. It generates project artifacts from a spec; it does not
give financial advice. Use it at your own risk.
