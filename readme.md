# Armbian Ubuntu Minimal — ROCK Pi 4A

Custom **Armbian Ubuntu Minimal** build for the **ROCK Pi 4A**.

The project provides a lightweight Ubuntu-based Armbian image without a desktop environment, intended for servers, headless systems, development, and embedded applications.

## Features

* **Board:** ROCK Pi 4A
* **Architecture:** ARM64
* **OS:** Ubuntu
* **Image:** Minimal
* **Desktop environment:** None
* **Armbian:** `v26.08`
* **Kernel branch:** `current`
* **Build:** Automated with GitHub Actions
* **Build environment:** Ubuntu 24.04

## Downloads

Pre-built images are available in the project's **GitHub Releases**.

Each release contains the generated Armbian image and related files.

## Installation

Download the latest `.img.xz` image from Releases.

### Linux

Extract and write the image to an SD card or other supported storage device:

```bash
xzcat Armbian_*.img.xz | sudo dd of=/dev/sdX bs=4M status=progress conv=fsync
```

Replace `/dev/sdX` with the correct device.

You can find the device using:

```bash
lsblk
```

> **Warning:** `dd` will overwrite all data on the selected device. Make absolutely sure that `/dev/sdX` points to the correct storage device.

### Verify the image

If a checksum file is provided with the release:

```bash
sha256sum -c Armbian_*.sha
```

Or calculate the checksum manually:

```bash
sha256sum Armbian_*.img.xz
```

## First Boot

Insert the prepared SD card into the ROCK Pi 4A and power it on.

The first boot may take some time while the system initializes.

After booting, connect to the device using SSH:

```bash
ssh root@<IP_ADDRESS>
```

Replace `<IP_ADDRESS>` with the IP address assigned to the ROCK Pi 4A.

## Building

The image can be built automatically using GitHub Actions.

Go to:

**GitHub → Actions → Build Armbian ROCK Pi 4A → Run workflow**

The workflow builds Armbian with the following configuration:

```text
BOARD=rockpi-4a
BRANCH=current
RELEASE=resolute
BUILD_DESKTOP=no
BUILD_MINIMAL=yes
BETA=no
KERNEL_CONFIGURE=no
KERNEL_GIT=shallow
```

After a successful build:

1. The generated images are uploaded as a GitHub Actions artifact.
2. A GitHub Release is created automatically.
3. The generated image files are attached to the release.

## Project Structure

```text
.
└── .github/
    └── workflows/
        └── build.yml
```

The build configuration is managed by the GitHub Actions workflow.

The actual Armbian build system is provided by the upstream Armbian project.

## Upstream Project

This project uses the Armbian build system:

* Armbian: https://github.com/armbian/build
* Armbian build branch: `v26.08`

## Disclaimer

This is a custom community build and is not an official Armbian release.

Use the images at your own risk. Always keep backups of important data before writing an image to a storage device.

## License

The build configuration in this repository follows the license of the respective files.

Armbian and its components are distributed under their respective open-source licenses.

---

**Target platform:** ROCK Pi 4A
**OS:** Ubuntu Minimal
**Architecture:** ARM64
