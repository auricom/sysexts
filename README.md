# sysexts

## Build

Install `cpio erofs-utils jq just podman`, then:

```sh
cd zen-browser
just targets
just build quay.io/fedora-ostree-desktops/base-atomic:45
```

Building needs root (via `sudo`) and podman. See [fedora-sysexts/community](https://github.com/fedora-sysexts/community) for details.
