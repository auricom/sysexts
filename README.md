# sysexts

## Build

Install `cpio erofs-utils jq just podman`, then:

```sh
cd zen-browser
just targets
just build quay.io/fedora-ostree-desktops/base-atomic:45
```

Building needs root (via `sudo`) and podman. See [fedora-sysexts/community](https://github.com/fedora-sysexts/community) for details.

Running the plain `just build` as your user fails at the SELinux relabel step
(`setfiles: Could not set context ...`): `sudo` creates files owned by real
root, which the rootless relabel container can not touch. Instead, from the
host with only `just`, `distrobox` and `podman` installed, build inside a
Debian distrobox (`sysext-builder`, created on first run):

```sh
cd zen-browser
just distrobox-build quay.io/fedora-ostree-desktops/base-atomic:45
```

`rootfs/` is then owned by a subuid: clean up from inside the box with
`distrobox enter sysext-builder -- just clean`, not from the host. Remove the
box with `distrobox rm sysext-builder`.

## Publishing

`.github/workflows/sysexts.yml` builds `zen-browser` for Fedora 43, 44 and 45
on x86_64 and aarch64, and pushes each build as an OCI artifact to
`ghcr.io/auricom/sysexts/zen-browser`:

- Pull requests only build.
- Pushes to `main` (and manual runs) rebuild and publish.
- A nightly run publishes only when the COPR has a new version.

Tags are `<version>-<fedora>-<arch>` (for example `1.24.1b-1.fc45-45-x86-64`)
plus a moving `<fedora>-<arch>` tag (for example `45-x86-64`). The first push
creates the package as private: make it public in the package settings to pull
it without logging in. Then install it with:

```sh
oras pull ghcr.io/auricom/sysexts/zen-browser:45-x86-64
sudo install -D -m0644 zen-browser-*.raw /var/lib/extensions/zen-browser.raw
sudo systemd-sysext refresh
```
