# Go

The Go binding links the C ABI via cgo. Construct a `Compiler` and drive it with
`Command(json) -> (json, error)`.

```bash
go get github.com/wickra-lib/wickra-compile-go
```

```go
package main

import (
	"fmt"

	wickra "github.com/wickra-lib/wickra-compile-go"
)

func main() {
	c := wickra.New()
	defer c.Close()

	resp, _ := c.Command(`{"cmd":"compile","dry_run":true,"spec":{
		"strategy":{"symbol":"x","timeframe":"1h",
			"indicators":{"f":{"type":"Ema","params":[3]}},
			"entry":{"cross_above":["f","f"]},"exit":{"cross_below":["f","f"]},
			"sizing":{"type":"fixed_qty","qty":1}},
		"target":{"kind":"wasm"},"crate_name":"demo"}}`)
	fmt.Println(resp) // response JSON, including manifest.project_hash
}
```

## More

- [pkg.go.dev/github.com/wickra-lib/wickra-compile-go](https://pkg.go.dev/github.com/wickra-lib/wickra-compile-go)
- [Source & examples](https://github.com/wickra-lib/wickra-compile/tree/main/examples/go)
