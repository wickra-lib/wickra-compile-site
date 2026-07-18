---
layout: home
title: Wickra Compile — a strategy spec into a standalone deployable
titleTemplate: false

hero:
  name: "Wickra Compile"
  text: "Write once as data. Deploy anywhere."
  tagline: "Compile a strategy spec into a standalone deployable — a WASM module, a self-contained binary, or a no_std artifact for microcontrollers. The spec is data, not code — and the manifest is byte-identical across ten languages."
  image:
    src: /wickra-mark.svg
    alt: Wickra Compile
  actions:
    - theme: brand
      text: View on GitHub
      link: https://github.com/wickra-lib/wickra-compile
    - theme: alt
      text: CompileSpec & targets
      link: https://github.com/wickra-lib/wickra-compile/blob/main/docs/SPEC.md
    - theme: alt
      text: API
      link: /api/rust

features:
  - icon: 📦
    title: Strategy in, deployable out
    details: You write your strategy as a CompileSpec — the same StrategySpec wickra-backtest runs — and the compiler generates a standalone Rust project that embeds it verbatim and calls the Wickra engine. No interpreter, no runtime spec parsing.
  - icon: 🎯
    title: Three targets
    details: "Emit a WASM module, a self-contained native binary, or a no_std artifact for a microcontroller from an allow-listed MCU set — one spec, whichever target you name."
  - icon: 🔒
    title: A reproducible manifest
    details: "The generated manifest — the list of files with their hashes plus the canonical spec hash (project_hash) — is byte-identical across all ten language bindings and reproducible across runs."
  - icon: 📈
    title: The Wickra engine, embedded
    details: "The generated project calls the same core that powers a backtest, so a compiled strategy sees exactly the same numbers over the 514 indicators of the Wickra core."
  - icon: 🌐
    title: Ten languages, one manifest
    details: "The compiler is a JSON-over-C-ABI data API (Compiler::command_json) in Rust, Python, Node.js, WASM, C, C++, C#, Go, Java and R. A developer in any language emits the same project."
  - icon: 🧪
    title: Deterministic, proven
    details: The same spec produces the byte-identical manifest here and in every other binding — the exact cross-language golden invariant, pinned by a golden corpus in CI.
---

<script setup>
const installTabs = [
  { label: 'Python', lang: 'bash', code: 'pip install wickra-compile' },
  { label: 'Node',   lang: 'bash', code: 'npm install wickra-compile' },
  { label: 'Rust',   lang: 'bash', code: 'cargo add wickra-compile' },
  { label: 'WASM',   lang: 'bash', code: 'npm install compile-wasm' },
  { label: 'C',      lang: 'bash', code: '# prebuilt header + library from GitHub releases:\n# github.com/wickra-lib/wickra-compile/releases' },
  { label: 'C#',     lang: 'bash', code: 'dotnet add package Wickra.Compile' },
  { label: 'Go',     lang: 'bash', code: 'go get github.com/wickra-lib/wickra-compile-go' },
  { label: 'Java',   lang: 'xml',  code: '<!-- Maven Central -->\n<dependency>\n  <groupId>org.wickra</groupId>\n  <artifactId>wickra-compile</artifactId>\n  <version>0.1.0</version>\n</dependency>' },
  { label: 'R',      lang: 'r',    code: 'install.packages("wickracompile", repos = "https://wickra-lib.r-universe.dev")' },
]

const pyCode = `import json
from wickra_compile import Compiler

spec = {
    "strategy": {
        "symbol": "x", "timeframe": "1h",
        "indicators": {"f": {"type": "Ema", "params": [3]}},
        "entry": {"cross_above": ["f", "f"]}, "exit": {"cross_below": ["f", "f"]},
        "sizing": {"type": "fixed_qty", "qty": 1},
    },
    "target": {"kind": "wasm"}, "crate_name": "demo",
}

c = Compiler()
resp = json.loads(c.command(json.dumps({"cmd": "compile", "dry_run": True, "spec": spec})))
print(resp["manifest"]["project_hash"])`

const nodeCode = `import { Compiler } from 'wickra-compile'

const spec = {
  strategy: {
    symbol: 'x', timeframe: '1h',
    indicators: { f: { type: 'Ema', params: [3] } },
    entry: { cross_above: ['f', 'f'] }, exit: { cross_below: ['f', 'f'] },
    sizing: { type: 'fixed_qty', qty: 1 },
  },
  target: { kind: 'wasm' }, crate_name: 'demo',
}

const c = new Compiler()
const resp = JSON.parse(c.command(JSON.stringify({ cmd: 'compile', dry_run: true, spec })))
console.log(resp.manifest.project_hash)`

const cliCode = `# Compile a strategy spec to a WASM project:
wickra-compile --spec strategy.json --target wasm --out ./dist

# Dry run — just the manifest, no files written:
wickra-compile --spec strategy.json --target wasm --dry-run`

const snippetTabs = [
  { label: 'Python', lang: 'python',     code: pyCode },
  { label: 'Node',   lang: 'javascript', code: nodeCode },
  { label: 'CLI',    lang: 'bash',       code: cliCode },
]
</script>

## The spec is JSON, not code

A compile is a `CompileSpec`: a `strategy` (the same `StrategySpec` a backtest
runs), a `target` and a `crate_name`. The compiler embeds the strategy verbatim
and generates a standalone project for the target you name.

```json
{
  "strategy": {
    "symbol": "BTCUSDT", "timeframe": "1h",
    "indicators": { "fast": { "type": "Ema", "params": [12] }, "slow": { "type": "Ema", "params": [26] } },
    "entry": { "cross_above": ["fast", "slow"] },
    "exit":  { "cross_below": ["fast", "slow"] },
    "sizing": { "type": "fixed_qty", "qty": 1 }
  },
  "target": { "kind": "wasm" },
  "crate_name": "my_strategy"
}
```

## Install

The same compiler from every language — native Rust, Python, Node.js and WASM,
plus a C ABI for C, C++, C#, Go, Java and R.

<InstallTabs :tabs="installTabs" />

## Compile from any language

Construct a `Compiler`, then drive it with `command(json) -> json`. A given spec
produces the byte-identical manifest in every binding.

<InstallTabs :tabs="snippetTabs" />

## Built on the Wickra core

Wickra Compile is part of the [Wickra](https://wickra.org) ecosystem. The project
it generates embeds [`wickra-core`](https://github.com/wickra-lib/wickra), so a
compiled strategy computes exactly the same indicator values a backtest or a live
chart would.

> Wickra Compile is a software library, not a trading system, and comes with no
> warranty — use at your own risk.
