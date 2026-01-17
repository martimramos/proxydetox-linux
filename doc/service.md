# Proxydetox as user service

Register Proxydetox as a user service such that it is automatically started by
the system when the user is logged in.

**Note:** These steps are only required when using `cargo install`. When
installing the provided packages these steps are not necessary.

## Automatically start Proxydetox with a user session

To automatically start `proxydetox` when a user session is active, we can
register it with `systemd(8)`.

Create a file `~/.config/systemd/user/proxydetox.service`, you can use
[`debian/proxydetox.service`][service] as a template, but make sure to update
the [`ExecStart`][execstart] part with an _absolute_ path.

To finally enable the service, use the following commands:

```sh
systemctl --user daemon-reload
systemctl --user enable proxydetox.service
systemctl --user start proxydetox.service
```

[service]: https://github.com/kiron1/proxydetox/blob/main/pkg/deb/proxydetox.service "proxydetox.service file"
[execstart]: https://man7.org/linux/man-pages/man5/systemd.service.5.html "man 5 systemd.service"
