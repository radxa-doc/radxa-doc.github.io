# Development

## Dependency

Arch/Manjaro:

```
# You need to install `yay` first since `fpm` is availabe in AUR
# Otherwise install `ruby` and follow Debian guide to install `fpm`
yay -Syu --noconfirm --needed base-devel aarch64-linux-gnu-gcc arm-none-eabi-gcc git uboot-tools cpio multipath-tools jq docker dpkg fpm 
```

Debian/Ubuntu:

We use `docker` provided from distro's own repository. If you installed `docker` from another source, please remove `docker.io` from `apt install` command.

```
sudo apt update
sudo apt install -y build-essential crossbuild-essential-arm64 gcc-arm-none-eabi git u-boot-tools cpio multipath-tools jq docker.io bison flex libssl-dev python2 ruby
sudo gem install fpm
```

## Additional system config

```
sudo usermod -a -G docker $USER
sudo systemctl enable docker
sudo reboot
```
