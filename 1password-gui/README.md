# 1password-gui

[1Password](https://1password.com/) desktop app, repacked from the official x86_64 RPM (no aarch64 build exists). The RPM signature is verified against 1Password's key during the build.

- 1Password ships in `/opt/1Password`, which a sysext can not provide, so the build moves it to `/usr/lib/1Password`.
- The browser helper `1Password-BrowserSupport` (and `1password-mcp`, when present) must be setgid `onepassword` (GID 1500) / `onepassword-mcp` (GID 1501), otherwise it aborts with "running without libc's security". The RPM scriptlets that do this never run for a sysext, so the build sets the group and mode in the image and `usr/lib/sysusers.d/1password-gui.conf` creates the groups with the same fixed GIDs on the host.
- `/etc/1password/custom_allowed_browsers` and the polkit policy are left to the host.
