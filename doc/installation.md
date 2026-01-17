# Install Proxydetox

## Linux

1. Download the [`proxydetox-*-x86_64-linux.deb`][releases] Debian package.
2. Install using the `dpkg` command on Debian-based platforms:
   ```sh
   sudo dpkg --install proxydetox-*-x86_64-linux.deb
   ```

### Register Proxydetox as systemd user daemon

The Debian package comes with a systemd service file.

Enabling Proxydetox and starting it can be done with the following commands:

```sh
systemctl --user daemon-reload
systemctl --user enable proxydetox
systemctl --user start proxydetox
```

To disable and stop it please use:

```sh
systemctl --user stop proxydetox
systemctl --user disable proxydetox
```

## From sources

To build Proxydetox from sources, please refer to the
[Build Proxydetox](./build.md) section.

[releases]: https://github.com/kiron1/proxydetox/releases/latest "Proxydetox releases"
