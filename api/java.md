# Java

The Java binding links the C ABI via a small JNI shim. Construct a `Compiler` and
drive it with `command(json) -> json`.

```xml
<!-- Maven Central -->
<dependency>
  <groupId>org.wickra</groupId>
  <artifactId>wickra-compile</artifactId>
  <version>0.1.0</version>
</dependency>
```

```java
import org.wickra.compile.Compiler;

try (Compiler c = new Compiler()) {
    String resp = c.command(
        "{\"cmd\":\"compile\",\"dry_run\":true,\"spec\":{"
      + "\"strategy\":{\"symbol\":\"x\",\"timeframe\":\"1h\","
      + "\"indicators\":{\"f\":{\"type\":\"Ema\",\"params\":[3]}},"
      + "\"entry\":{\"cross_above\":[\"f\",\"f\"]},\"exit\":{\"cross_below\":[\"f\",\"f\"]},"
      + "\"sizing\":{\"type\":\"fixed_qty\",\"qty\":1}},"
      + "\"target\":{\"kind\":\"wasm\"},\"crate_name\":\"demo\"}}");
    System.out.println(resp);
}
```

## More

- [central.sonatype.com/artifact/org.wickra/wickra-compile](https://central.sonatype.com/artifact/org.wickra/wickra-compile)
- [Source & examples](https://github.com/wickra-lib/wickra-compile/tree/main/examples/java)
