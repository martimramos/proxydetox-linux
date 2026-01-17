# Introduction to Proxydetox

A small proxy to relieve the pain of some corporate proxies.

Proxydetox can act as an intermediate HTTP proxy for your local applications and
the actual HTTP proxy. Proxydetox will talk to the actual corporate HTTP proxies
on behalf of the actual application. Proxydetox will select the correct upstream
proxy based on the [Proxy Auto-Configuration (PAC) file][mdnpac] provided by the
network administrator and will take care to correctly authenticate against the
upstream proxy.

With Proxydetox in place, most local applications can be configured to use the
proxy by setting the environment variables `http_proxy` and `https_proxy`.

The following authentication methods are supported:

- [Basic][basic]: use the username and password from `~/.netrc`.
- [Negotiate][negotiate]: uses [GSSAPI][gssapi] for Kerberos authentication.

Proxydetox supports Linux and other POSIX-compliant systems (tested on Ubuntu
and OpenBSD).

Pre-built versions of Proxydetox can be found on [the releases page][releases].
Installation instructions are provided in the
[installation section](installation.md).

[mdnpac]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Proxy_servers_and_tunneling/Proxy_Auto-Configuration_(PAC)_file "Proxy Auto-Configuration (PAC) file"
[basic]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication#basic_authentication_scheme "Basic authentication scheme"
[negotiate]: https://www.rfc-editor.org/rfc/rfc4559.html#section-4 "HTTP Negotiate Authentication Scheme"
[gssapi]: https://web.mit.edu/kerberos/krb5-devel/doc/appdev/gssapi.html "Generic Security Services API (GSSAPI)"
[releases]: https://github.com/kiron1/proxydetox/releases "Proxydetox releases"

## License

This source code is under the [MIT](https://opensource.org/licenses/MIT) license
with the exceptions mentioned in "Third party source code in this repository".
