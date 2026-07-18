# R

The R package links the C ABI. Build a compiler with `wkcompile_new`, then drive
it with `wkcompile_command`.

```r
install.packages("wickracompile", repos = "https://wickra-lib.r-universe.dev")
```

```r
library(wickracompile)

spec <- '{"cmd":"compile","dry_run":true,"spec":{
  "strategy":{"symbol":"x","timeframe":"1h",
    "indicators":{"f":{"type":"Ema","params":[3]}},
    "entry":{"cross_above":["f","f"]},"exit":{"cross_below":["f","f"]},
    "sizing":{"type":"fixed_qty","qty":1}},
  "target":{"kind":"wasm"},"crate_name":"demo"}}'

c <- wkcompile_new()
resp <- wkcompile_command(c, spec)
cat(resp)
```

## More

- [wickra-lib.r-universe.dev](https://wickra-lib.r-universe.dev)
- [Source & examples](https://github.com/wickra-lib/wickra-compile/tree/main/examples/r)
