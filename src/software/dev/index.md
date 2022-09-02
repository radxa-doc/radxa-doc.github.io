# Development

## Dependency

Arch/Manjaro:

```
sudo pacman -Syu --noconfirm --needed base-devel aarch64-linux-gnu-gcc arm-none-eabi-gcc git uboot-tools cpio multipath-tools jq docker dpkg swig bc dtc inetutils rsync
# `fpm` from AUR is currently broken, otherwise you can install it with yay
sudo pacman -S rubygems
gem install fpm
```

Debian/Ubuntu:

We use `docker` provided from distro's own repository. If you installed `docker` from another source, please remove `docker.io` from `apt install` command.

```
sudo apt update
sudo apt install -y build-essential crossbuild-essential-arm64 gcc-arm-none-eabi git u-boot-tools cpio multipath-tools jq docker.io bison flex libssl-dev python2 ruby swig python2-dev
sudo gem install fpm
```

## Additional system config

```
sudo usermod -a -G docker $USER
sudo systemctl enable docker
sudo reboot
```
