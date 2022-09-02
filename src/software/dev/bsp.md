# lbuild

## `fork.conf`

`fork.conf` is the kernel fork configuration file. This file is mandatory and is sourced early by `lbuild`. You can override many options but below are some most commonly used (and supported) settings for this file:

`LINUX_GIT` Specify upstream kernel repo.

`LINUX_COMMIT` or `LINUX_BRANCH` or `LINUX_TAG` Specify the exact kernel revision. The first defined option in the listed order will be used.

`LINUX_DEFCONFIG` Specify the defconfig used for building. Default to `defconfig`.

`SUPPORTED_BOARDS` Specify the supported boards list, which is a [Bash array](https://www.gnu.org/software/bash/manual/html_node/Arrays.html).

## `kconfig.conf`

`kconfig.conf` is a kernel configuration file. This file mirrors `defconfig` format.
