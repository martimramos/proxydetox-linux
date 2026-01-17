# Proxydetox Linux

**A Linux-focused fork of [proxydetox](https://github.com/kiron1/proxydetox)**

---

## About This Fork

This is a fork of the excellent [proxydetox](https://github.com/kiron1/proxydetox) project created by [kiron1](https://github.com/kiron1). All credit for the original design and implementation goes to the original author.

This fork removes macOS and Windows support to create a leaner, Linux-only codebase with a focus on WSL (Windows Subsystem for Linux) environments.

---

## The Problem: Corporate Proxy Hell

If you've ever worked behind a corporate proxy, you know the pain:

- **NTLM authentication** - because apparently we're still living in 2003
- **Kerberos/SPNEGO** - "just get a ticket", they said. "It'll be easy", they said
- **PAC files** - JavaScript deciding your network fate
- **Proxy chains** - proxies behind proxies behind proxies
- Your CLI tools crying because `curl` doesn't speak corporate

Most command-line tools only understand simple `http_proxy` environment variables. They don't negotiate NTLM. They don't do Kerberos. They just fail silently while you question your career choices.

**Proxydetox sits between your tools and the corporate nightmare**, handling all the authentication so your applications don't have to.

## How It Works

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   Your Tools    │────▶│   Proxydetox    │────▶│ Corporate Proxy │
│  (curl, apt,    │     │  localhost:3128 │     │  (NTLM/Kerberos)│
│   docker, etc)  │     │                 │     │                 │
└─────────────────┘     └─────────────────┘     └─────────────────┘
        │                       │                       │
        │  http_proxy=          │  Handles PAC files    │
        │  localhost:3128       │  Negotiates auth      │
        │                       │  Manages sessions     │
```

Proxydetox:
1. Reads your corporate [PAC file][mdnpac] to determine which proxy to use
2. Handles [Negotiate (SPNEGO/Kerberos)][negotiate] or [Basic][basic] authentication
3. Exposes a simple local proxy that your tools can actually use

## Features

- **PAC file support** - Automatically routes traffic based on your corporate PAC file
- **Kerberos/SPNEGO authentication** - Uses your existing Kerberos tickets
- **Basic authentication** - Via `.netrc` file
- **Systemd integration** - Socket activation support for proper service management
- **Lightweight** - Written in Rust, minimal resource usage

## Quick Start

```bash
# Set up your Kerberos ticket
kinit your.username@CORP.DOMAIN.COM

# Run proxydetox with SPNEGO authentication
proxydetox --negotiate --pac-file http://proxy.corp.com/proxy.pac

# Configure your shell
export http_proxy=http://127.0.0.1:3128
export https_proxy=http://127.0.0.1:3128

# Now your tools just work
curl https://example.com
apt update
docker pull ubuntu
```

## Installation

### Debian/Ubuntu

Download the `.deb` package from the [releases](https://github.com/kiron1/proxydetox/releases) page:

```bash
sudo dpkg -i proxydetox-*.deb
```

### Build from Source

```bash
# Install build dependencies
sudo apt install libclang-dev libkrb5-dev

# Build with Kerberos/SPNEGO support (default)
cargo build --release

# Or build without Kerberos support
cargo build --release --no-default-features
```

## Documentation

See the [original documentation](https://proxydetox.colorto.cc/) for detailed configuration options.

## Credits and Attribution

This project is a fork of [proxydetox](https://github.com/kiron1/proxydetox).

**Original Author:** [kiron1](https://github.com/kiron1)

The original proxydetox is a well-designed, cross-platform solution supporting macOS, Windows, and Linux. This fork strips out the non-Linux code to maintain a simpler codebase focused on Linux and WSL environments.

If you need cross-platform support, please use the [original project](https://github.com/kiron1/proxydetox).

## License

This source code is under the [MIT](https://opensource.org/licenses/MIT) license with the exceptions mentioned in "Third party source code in this repository".

See the original project for full license details.

---

[mdnpac]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_(PAC)_file "Proxy Auto-Configuration (PAC) file"
[basic]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication#basic_authentication_scheme "Basic authentication scheme"
[negotiate]: https://www.rfc-editor.org/rfc/rfc4559.html#section-4 "HTTP Negotiate Authentication Scheme"
