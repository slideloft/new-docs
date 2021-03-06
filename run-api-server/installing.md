---
title: Installing
order: 20
---

# installing

import { CodeExample } from "components/CodeExample";

To install Horizon, you have a choice: you can download a [prebuilt release for your target architecture](https://github.com/stellar/go/releases) and operation system or you can [build Horizon yourself](installing.md#Building). When either approach is complete, you will find yourself with a directory containing a file named `horizon`. This file is a native binary.

After building or unpacking Horizon, you simply need to copy the native binary into a directory that is part of your PATH. Most unix-like systems have `/usr/local/bin` in PATH by default, so unless you have a preference or know better, we recommend you copy the binary there.

To test the installation, simply run `horizon --help` from a terminal. If the help for Horizon is displayed, your installation was successful. Note: some shells, such as zsh, cache PATH lookups. You may need to clear your cache \(by using `rehash` in zsh, for example\) before trying to run `horizon --help`.

## Building

Should you decide not to use one of our prebuilt releases, you may instead build Horizon from source. To do so, you need to install some developer tools:

* A unix-like operating system with the common core commands \(cp, tar, mkdir, bash, etc.\)
* A compatible distribution of Go \(Go 1.13 or later\)
* [git](https://git-scm.com/)
* [mercurial](https://www.mercurial-scm.org/)
* See the details in [README.md](https://github.com/stellar/go/blob/master/README.md#dependencies) for installing dependencies.
* Compile the Horizon binary: `go install github.com/stellar/go/services/horizon`. You should see the `horizon` binary in `$GOPATH/bin`.
* Add Go binaries to your PATH in your `bashrc` or equivalent, for easy access: `export PATH=${GOPATH//://bin:}/bin:$PATH`

Open a new terminal. Confirm everything worked by running `horizon --help` successfully.

Note: Building directly on windows is not supported.

