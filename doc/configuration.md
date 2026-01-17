# Configuration

## File locations

The following files are read during startup by Proxydetox. These files can be
used to tweak the behaviour of Proxydetox.

- `proxydetoxrc`: Main configuration file.
- `proxy.pac`: The PAC file, which defines the rules to select the correct
  upstream proxy.
- `.netrc`: Contains the authentication information when `--negotiate` is _not_
  used.

The configuration files are searched at the following locations:

The `.netrc` file is expected to be located in the `HOME` directory. If needed,
the location can be specified via the `--netrc-file` flag when invoking
Proxydetox.

The configuration files `proxydetoxrc` and `proxy.pac` are searched at user
configurable locations and system wide locations.

User configurable location:

- `~/.config/proxydetox/`

System wide locations:

- `/usr/etc/proxydetox`
- `/usr/local/etc/proxydetox/`
- `/opt/proxydetox/etc/`

## `proxydetoxrc` file format

The `proxydetoxrc` file lists all options which are usually provided via the
command line to `proxydetox`.

### Example

```sh
proxydetox --negotiate --listen 127.0.0.1:8080 --pac-file http://example.org/proxy.pac
```

Is equivalent with a `proxydetoxrc` file at one of the well known locations
listed above with the following content:

```
--negotiate
--listen 127.0.0.1:8080
--pac-file http://example.org/proxy.pac
```

## Negotiate authentication

To enable the Negotiate authentication the `--negotiate` flag must be added when
calling `proxydetox` or added to the `proxydetoxrc` configuration file.

## Basic authentication

When the basic authentication shall be used (default), the credentials are read
from the `~/.netrc` file. An example `~/.netrc` file will look as follows:

```
machine proxy.example.org
login ProxyUsername
password ProxyPassword
```

The basic authentication is insecure, since it requires storing the password in
clear text on disk and the password is transferred unencrypted.

## Proxy Auto-Configuration (PAC) file

A copy of the PAC file `proxy.pac` must be placed in one of the directories
searched by Proxydetox or specified via the `--pac-file` option. The PAC file
can also be a HTTP URL. The content will then be downloaded from the given
location.

The PAC file is usually maintained by the network administrators. The path
(usually some http location in the intranet) can be retrieved from the settings
of the pre-configured internet browser.

### Examples

```sh
proxydetox --pac-file http://example.org/proxy.pac
```

```sh
proxydetox --pac-file /tmp/test.pac
```

## Configuration options

The full list of configuration options can be retrieved with:

```sh
proxydetox --help
```
