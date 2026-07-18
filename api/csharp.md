# C\#

The .NET binding wraps the C ABI. Construct a `Compiler` and drive it with
`Command(json) -> json`.

```bash
dotnet add package Wickra.Compile
```

```csharp
using Wickra.Compile;

using var c = new Compiler();
var resp = c.Command(
    "{\"cmd\":\"compile\",\"dry_run\":true,\"spec\":{" +
    "\"strategy\":{\"symbol\":\"x\",\"timeframe\":\"1h\"," +
    "\"indicators\":{\"f\":{\"type\":\"Ema\",\"params\":[3]}}," +
    "\"entry\":{\"cross_above\":[\"f\",\"f\"]},\"exit\":{\"cross_below\":[\"f\",\"f\"]}," +
    "\"sizing\":{\"type\":\"fixed_qty\",\"qty\":1}}," +
    "\"target\":{\"kind\":\"wasm\"},\"crate_name\":\"demo\"}}");
Console.WriteLine(resp);
```

## More

- [nuget.org/packages/Wickra.Compile](https://www.nuget.org/packages/Wickra.Compile)
- [Source & examples](https://github.com/wickra-lib/wickra-compile/tree/main/examples/csharp)
