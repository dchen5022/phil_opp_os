# Rust OS
Based on the blog at https://os.phil-opp.com.

# Setup
Nightly Rust compiler is required to use features like `json-target-spec`.
To use the nightly compiler for this project:
`rustup override set nightly`

The nightly toolchain for x86_64-unknown-linux-gnu is also required:
`rustup component add rust-src --toolchain nightly-x86_64-unknown-linux-gnu`
This allows recompiling `core` and `compiler_builtins` for the custom target.
`unstable.build-std` requires the nightly from at least 2020-07-15.

The `bootimage` tool is also required to link the bootloader provided by the
`bootloader` crate to the kernel into a bootable disk image. Install with:
`cargo install bootimage`

`bootimage` also requires the `llvm-tools-preview` rustup component.
`rustup component add llvm-tools-preview`.

# Building and running
The build target is set to x86_64-phil_opp_os in .cargo/config.toml, so you can
build the kernel binary with just `cargo build`.

To create a bootable disk image, run `cargo bootimage`, which builds the
kernel, the bootloader, and then combines into a bootable disk image. The image
can be found at `target/x86_64-phil_opp_os/debug/bootimage-phil_opp_os.bin`

The bootable disk image is run by QEMU by default using `qemu-system-x86_64`.
`cargo run` creates the bootable disk image and then boots in QEMU.
`cargo test` runs the image in a headless QEMU instance.

