# shadowsocks-build

This repository builds shadowsocks-libev and its dependencies for use in Desktop.

Since this repository uses submodules, make sure to include `--recursive` when cloning it.  If you forgot, `git submodule update --init --recursive` will initialize the submodules.

# Included dependencies

The repo builds libpcre, libsodium, mbedtls, c-ares, and libev from source as dependencies of shadowsocks-libev.

There are two `libev` submodules.  On Windows, shadowsocks-libev requires a modified libev from a specific branch, `libev-windows/libev` points to this branch.  `libev-posix/libev` is used on other platforms.

# Build environment

This project builds on Linux, Mac OS, and Windows; artifacts are statically linked.  Linux builds should be made on Ubuntu 16.04 to ensure they will run on 16.04 and later.

## Dependencies to check

Do we need:

* autotools package? (probably on MinGW)
* gettext?
* pkg-config?
* asciidoc?
* xmlto?

## Ubuntu

You will need the following dependencies:

* build-essential
* git
* automake
* libtool

## Mac

Install the Xcode command-line tools.

Install Homebrew from https://brew.sh and the following packages:

* autoconf
* automake
* libtool
* python@2

## Windows

1. Install MSYS2 from https://www.msys2.org - follow the instructions on that page
2. Install dependencies
   * x86_64: `pacman -S base-devel mingw-w64-x86_64-toolchain git mingw-w64-x86_64-crt-git`
   * x86: `pacman -S base-devel mingw-w64-i686-toolchain git mingw-w64-i686-crt-git`
   * If prompted by pacman for group members, accept defaults (all members in group)
3. Clone `shadowsocks-build` recursively _from the MSYS2 shell_.  Don't use Git for Windows, it handles line endings differently and will cause issues.
   * `git clone --recursive https://github.com/pia-foss/desktop-shadowsocks.git`

On Windows, building from the MSYS2 MinGW 64-bit shell produces a 64-bit build, building in the MSYS2 MinGW 32-bit shell produces a 32-bit build.

# Build

To build, just run `./build-posix` (even on Windows).  `pia-ss-local` is generated in `./out/artifacts/<platform>/`.

# Submodules, patches, updating dependencies

This project includes dependencies as submodules; patches are applied at build time.

The preferred way to work on the submodule patches is to apply them to the submodule, work in the submodule and commit to Git (locally), then regenerate patches.  See https://github.com/pia-foss/desktop-openvpn#working-on-module-patches.
