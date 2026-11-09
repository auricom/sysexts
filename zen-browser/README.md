# zen-browser

[Zen Browser](https://zen-browser.app/), packaged from the [`sneexy/zen-browser`](https://copr.fedorainfracloud.org/coprs/sneexy/zen-browser/) COPR. The COPR is an unofficial repack of the upstream binaries.

- Zen ships in `/opt/zen`, which a sysext can not provide, so the build moves it to `/usr/lib/zen` and repoints the `zen-browser` wrapper and the icon symlinks.
- The package ships `/usr/lib/zen/distribution/policies.json`, which is meant to disable in-app updates: update the sysext instead.

## Status

Built for Fedora 45 x86_64 (zen-browser 1.24.1b). The `zen-browser` RPM is the only package downloaded: the base image already provides its dependencies. The result has no `/opt` left and the wrapper and icons point to `/usr/lib/zen`.

Not tested: running the merged sysext, and aarch64.
