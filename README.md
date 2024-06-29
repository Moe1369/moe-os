# moe-os &nbsp; [![build-ublue](https://github.com/moe1369/moe-os/actions/workflows/build.yml/badge.svg)](https://github.com/moe1369/moe-os/actions/workflows/build.yml)

Custom Fedora Image made with [BlueBuild](https://blue-build.org).
For personal use based on [ublue-os Silverblue main Variant](https://github.com/ublue-os/main/)

This is meant to somewhat emulate bazzite while keeping things "clean". Used as a daily driver for general usage and secondarily for couch gaming.

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

### Return to Gaming Mode doesn't work

Nobaras Package expects a qdbus binary but kinoite installs it as qdbus-qt6.

Create a new Folder under your home and symlink the binary under a new name.
```
mkdir bin \
ln -s /usr/bin/qdbus-qt6 /var/home/YOURUSERNAME/bin/qdbus
```

### Steam Deck Mode won't update OOBE

Login to Plasma and complete OOBE once in nested gamescope
```
 gamescope -e -- steam -steamdeck
```

### Wrong keyboard layout

Apparently one of the images defaults to en_US Keyboard Layout. Change it back in Plasma Settings.

### Steam in Desktop Mode flashes on and off

This happens in multi GPU setups which are becoming more common. 

Go into Plasma Menu Editor, copy and paste Steam Desktop File and keep the name the same.

Open your .desktop File and change the value to false as seen in the screenshot.

![grafik](https://github.com/Moe1369/moe-os/assets/65728018/b9346111-81f3-4886-9808-49354378feb4)
