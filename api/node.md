# Node.js

The Node package is a native napi addon over the Rust core. Construct a `Compiler`
and drive it with `command(json) -> json`.

```bash
npm install wickra-compile
```

```javascript
import { Compiler } from 'wickra-compile'

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
console.log(resp.manifest.project_hash)
```

## More

- [npmjs.com/package/wickra-compile](https://www.npmjs.com/package/wickra-compile)
- [Source & examples](https://github.com/wickra-lib/wickra-compile/tree/main/examples/node)
