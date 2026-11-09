# zen-browser

[Zen Browser](https://zen-browser.app/), packaged from the [`sneexy/zen-browser`](https://copr.fedorainfracloud.org/coprs/sneexy/zen-browser/) COPR. The COPR is an unofficial repack of the upstream binaries.

- Zen ships in `/opt/zen`, which a sysext can not provide, so the build moves it to `/usr/lib/zen` and repoints the `zen-browser` wrapper and the icon symlinks.
- The package ships `/usr/lib/zen/distribution/policies.json`, which is meant to disable in-app updates: update the sysext instead.

Not yet built or run: the `rpms/` dependency pull-in result is still to be recorded here after the first build.
