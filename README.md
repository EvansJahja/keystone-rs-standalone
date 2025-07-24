# keystone-rs-standalone

Yet another Rust binding for [Keystone](http://www.keystone-engine.org/) assembler framework.

Keystone is included as a submodule.

This is a fork from https://github.com/tathanhdinh/keystone-rs which does not seem to be maintained anymore.

Currently, this builds on Windows.

## Building

This project requires LLVM. Tested on Windows 10 with LLVM-18.1.8.

## Cloning

This project contains submodule, i.e. 

`git clone --recurse-submodules https://github.com/EvansJahja/keystone-rs-standalone.git`

## Features
 - Hierarchical architecture: low-level binding is done by [keystone-sys](keystone-sys)
 - Fully wrapped and reexported types: no more low-level stuffs
 - Zero-copy: no additional memory allocation
 - Windows support

## Sample
```rust
use keystone::*;

fn main() {
    let engine = Keystone::from(Arch::X86, Mode::Bit32)
        .expect("Unable to initialize Keystone engine");

    engine.option(OptionType::Syntax, OptionValue::SyntaxNasm)
        .expect("Unable to set NASM syntax");

    let asm = engine.asm("mov ebp, esp", 0x4000)
        .expect("Unable to assemble");

    println!("{}", asm);
}
```

## Contributors
 - [@mteyssier](https://github.com/mteyssier)
 - [@Bobo1239](https://github.com/Bobo1239)

## Acknowledgments
 - Remco Verhoef (@remco_verhoef) for the [original work](https://github.com/keystone-engine/keystone/tree/master/bindings/rust)
 - Some wrapper macros from [capstone-rs](https://github.com/capstone-rust/capstone-rs)
 - @tathanhdinh for [including keystone-sys](https://github.com/tathanhdinh/keystone-rs)
