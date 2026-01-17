# Building Proxydetox

Proxydetox can be built using [cargo][cargo].

[cargo]: https://doc.rust-lang.org/cargo/ "Cargo is the Rust package manager"

## Using cargo

The easiest way is to use `cargo` from [rustup][rustup]. The next command will
install the `proxydetox` binary in `~/.cargo/bin`.

```sh
cargo install --git https://github.com/kiron1/proxydetox.git
```

If you have cloned this repository already, you can also do:

```sh
cargo install --path .
```

[rustup]: https://rustup.rs/ "rustup.rs - The Rust toolchain installer"

### Enable build features

To enable the Negotiate authentication method, the `negotiate` feature must be
enabled. This means we would need to add `--features negotiate` to the above
`cargo install ...` command.

On GNU/Linux the
[Generic Security Services Application Program Interface (GSSAPI)][gssapi] is
used.

[gssapi]: https://en.wikipedia.org/wiki/Generic_Security_Services_Application_Program_Interface

## Autostart

To start Proxydetox automatically when a user is logged in, please see the
[Autostart](service.md) section.
