# ppc32-builds

CI/CD build configurations to get binaries for projects on 32-Bit PowerPC (ppc32) and other "esoteric" environments.

[![hydrun CI](https://github.com/pojntfx/ppc32-builds/actions/workflows/hydrun.yaml/badge.svg)](https://github.com/pojntfx/ppc32-builds/actions/workflows/hydrun.yaml)
[![Matrix](https://img.shields.io/matrix/ppc32-builds:matrix.org)](https://matrix.to/#/#ppc32-builds:matrix.org?via=matrix.org)
[![Binary Downloads](https://img.shields.io/github/downloads/pojntfx/ppc32-builds/total?label=binary%20downloads)](https://github.com/pojntfx/ppc32-builds/releases)

## Overview

Many modern toolchains, such as Go, don't work on PowerPC 32 and other "esoteric" environments. It can thus become quite hard to build and use software on these machines, even if cross-compilation is a possibility. This repo intends to produce and vendor pre-built static binaries for these platforms, so that they may still be used in the 21st century.

Currently, the following apps are set up to be built every week:

- [gokcehan/lf](https://github.com/gokcehan/lf)
- [OJ/gobuster](https://github.com/OJ/gobuster)
- [ffuf/ffuf](https://github.com/ffuf/ffuf)

If you want another app to be built, please [open a GitHub issue](https://github.com/pojntfx/ppc32-builds/issues/new).

## Installation

Static binaries are available on [GitHub releases](https://github.com/pojntfx/ppc32-builds/releases).

On Linux, you can install them like so:

```shell
$ export BIN=lf # Or gobuster etc.
$ curl -L -o /tmp/${BIN} "https://github.com/pojntfx/ppc32-builds/releases/latest/download/${BIN}.linux-$(uname -m)"
$ sudo install /tmp/${BIN} /usr/local/bin
```

On macOS, you can use the following:

```shell
$ export BIN=lf # Or gobuster etc.
$ curl -L -o /tmp/${BIN} "https://github.com/pojntfx/ppc32-builds/releases/latest/download/${BIN}.darwin-$(uname -m)"
$ sudo install /tmp/${BIN} /usr/local/bin
```

On Windows, the following should work (using PowerShell as administrator):

```shell
PS> $BIN=lf # Or gobuster etc.
PS> Invoke-WebRequest "https://github.com/pojntfx/ppc32-builds/releases/latest/download/$BIN.windows-x86_64.exe" -OutFile \Windows\System32\$BIN.exe
```

You can find binaries for more operating systems and architectures on [GitHub releases](https://github.com/pojntfx/ppc32-builds/releases).

## Contributing

To contribute, please use the [GitHub flow](https://guides.github.com/introduction/flow/) and follow our [Code of Conduct](./CODE_OF_CONDUCT.md).

To build any of the vendored apps locally, run:

```shell
$ git clone https://github.com/pojntfx/ppc32-builds.git
$ cd ppc32-builds
$ hydrun -o golang:bullseye './Hydrunfile go lf' # Build lf (or gobuster etc.) with Go
$ hydrun -o ghcr.io/pojntfx/bagccgop-base-sid -e '--privileged' './Hydrunfile gccgo lf' # Build lf (or gobuster etc.) with `gccgo`
$ out/out/lf.linux-x86_64
```

Have any questions or need help? Chat with us [on Matrix](https://matrix.to/#/#ppc32-builds:matrix.org?via=matrix.org)!

## License

ppc32-builds (c) 2022 Felix Pojtinger and contributors

SPDX-License-Identifier: AGPL-3.0
