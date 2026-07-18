# Rust

The native crate. Compile a `CompileSpec` with `compile`, or drive a `Compiler`
handle with the JSON command protocol every other binding uses.

```bash
cargo add wickra-compile
```

```rust
use compile_core::{compile, CompileSpec};

let spec = CompileSpec::from_json(SPEC).expect("valid spec");
let generated = compile(&spec).expect("compile");

println!("{}", generated.manifest.project_hash);
```

## More

- [crates.io/crates/wickra-compile](https://crates.io/crates/wickra-compile) - [docs.rs](https://docs.rs/wickra-compile)
- [Source & examples](https://github.com/wickra-lib/wickra-compile/tree/main/examples/rust)
- [CompileSpec & targets](https://github.com/wickra-lib/wickra-compile/blob/main/docs/SPEC.md)
