# recur

[Recur](https://recur.build/), packaged from the upstream RPM published in [`celestiaorg/recur-releases`](https://github.com/celestiaorg/recur-releases). The build downloads the latest release and checks it against the release `SHA256SUMS`. No Fedora package is downloaded: the base image must already provide the dependencies of the Recur RPM (GTK 4, WebKitGTK 6.0, GStreamer, Vulkan loader).

- Recur ships in `/opt/recur`, which a sysext can not provide, so the build moves it to `/usr/lib/recur` and repoints the `recur` symlink and the desktop entry.
- Recur has its own updater (see `manifest.json` in the releases): update the sysext instead.

## Status

Not built or tested yet.
