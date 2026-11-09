# resilio-sync

[Resilio Sync](https://www.resilio.com/sync/), packaged from the `resilio-sync` RPM of the upstream signed repository (`https://linux-packages.resilio.com/resilio-sync/rpm/<arch>`). The build imports its GPG key and downloads the package with `dnf`.

- The RPM ships its units in `/lib`, which the build merges into `/usr/lib`; the SysV init script is dropped.
- The RPM creates the `rslsync` user and `/var/lib/resilio-sync` in its scriptlets, which are not run here: `usr/lib/sysusers.d` and `usr/lib/tmpfiles.d` do it instead, and copy the default config from `/usr/etc/resilio-sync` to `/etc/resilio-sync`.
- Nothing is enabled by default. After the first `systemd-sysext refresh`:

```sh
sudo systemd-sysusers
sudo systemd-tmpfiles --create
sudo systemctl enable --now resilio-sync.service   # or: systemctl --user enable --now resilio-sync.service
```

## Status

Not built or tested yet.
