# kindle-tools

## kindle-gcc

`kindle-gcc` is a wrapper script that allows you to cross-compile C/C++ code for ARM (Kindle) devices using an Alpine Linux rootfs, QEMU, and proot. It automates the setup and compilation process, making it easy to build binaries for Kindle devices on any Linux host.

### Features
- Automatic download and setup of an Alpine Linux ARM rootfs
- Installs GCC and musl-dev in the rootfs if missing
- Transparently copies your source files into the rootfs, compiles them, and copies the output back

### Installation

To install `kindle-gcc` system-wide:

```sh
curl -fsSL https://raw.githubusercontent.com/gingrspacecadet/kindle-tools/refs/heads/main/kindle-gcc | sudo tee /usr/bin/kindle-gcc > /dev/null
sudo chmod +x /usr/bin/kindle-gcc
```

You will also need to have `proot` and `qemu-arm` installed on your system. On Arch Linux:

```sh
sudo pacman -S proot qemu-user-static
```

### Usage

Compile a C file for Kindle:

```sh
kindle-gcc hello.c -o hello
```

All arguments are passed through to GCC inside the ARM rootfs. The output file (if specified with `-o`) will be copied back to your current directory.

### How it works
1. Checks for an Alpine ARM rootfs in `~/alpine-rootfs`. If missing, downloads and sets it up.
2. Ensures GCC and musl-dev are installed in the rootfs.
3. Copies your input files to `/tmp` in the rootfs, runs GCC, and copies the output back.
4. Uses proot and QEMU to emulate ARM binaries on your host.

### Troubleshooting
- If you see permission errors, ensure you have write access to the output directory and that `/usr/bin/kindle-gcc` is executable.
- If proot or qemu-arm are missing, install them with your package manager.

### License
MIT
