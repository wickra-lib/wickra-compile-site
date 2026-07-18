# Python

The Python package wraps the Rust core over the C ABI. Construct a `Compiler` and
drive it with `command(json) -> json`.

```bash
pip install wickra-compile
```

```python
import json
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
print(resp["manifest"]["project_hash"])
```

## More

- [pypi.org/project/wickra-compile](https://pypi.org/project/wickra-compile/)
- [Source & examples](https://github.com/wickra-lib/wickra-compile/tree/main/examples/python)
