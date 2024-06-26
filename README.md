# moe-os &nbsp; [![build-ublue](https://github.com/moe1369/moe-os/actions/workflows/build.yml/badge.svg)](https://github.com/moe1369/moe-os/actions/workflows/build.yml)

Custom Fedora Image made with [BlueBuild](https://blue-build.org).
For personal use based on [ublue-os Kinoite main Variant](https://github.com/ublue-os/main/)

## Installation

To rebase an existing atomic Fedora installation to the latest build:

- First rebase to the unsigned image, to get the proper signing keys and policies installed:
  ```
  rpm-ostree rebase ostree-unverified-registry:ghcr.io/moe1369/moe-os:latest
  ```
- Reboot to complete the rebase:
  ```
  systemctl reboot
  ```
- Then rebase to the signed image, like so:
  ```
  rpm-ostree rebase ostree-image-signed:docker://ghcr.io/moe1369/moe-os:latest
  ```
- Reboot again to complete the installation
  ```
  systemctl reboot
  ```

The `latest` tag will automatically point to the latest build. That build will still always use the Fedora version specified in `recipe.yml`, so you won't get accidentally updated to the next major version.
## Pitfalls & common issues

Return to Gaming Mode doesn't work
Nobaras Package expects a qdbus binary but kinoite installs it as qdbus-qt6.

Create a new Folder under your home and symlink the binary under a new name.
```
mkdir bin
ln -s /usr/bin/qdbus-qt6 /var/home/YOURUSERNAME/bin/qdbus
```
