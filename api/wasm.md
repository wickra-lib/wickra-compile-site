# WASM

The WebAssembly build runs the same Rust core in the browser or any WASM runtime.
Construct a `Compiler` and drive it with `command(json) -> json`.

```bash
npm install compile-wasm
```

```javascript
import init, { Compiler } from 'compile-wasm'

await init() // fetches and instantiates the .wasm module

const c = new Compiler()
const spec = { strategy: { symbol: 'x', timeframe: '1h',
  indicators: { f: { type: 'Ema', params: [3] } },
  entry: { cross_above: ['f', 'f'] }, exit: { cross_below: ['f', 'f'] },
  sizing: { type: 'fixed_qty', qty: 1 } }, target: { kind: 'wasm' }, crate_name: 'demo' }
const resp = JSON.parse(c.command(JSON.stringify({ cmd: 'compile', dry_run: true, spec })))
console.log(resp.manifest.project_hash)
```

The same spec yields a manifest byte-identical to the native build. See the
[live demo](/demo) for the Wickra core running in your browser.

## More

- [npmjs.com/package/compile-wasm](https://www.npmjs.com/package/compile-wasm)
- [Source & examples](https://github.com/wickra-lib/wickra-compile/tree/main/bindings/wasm)
