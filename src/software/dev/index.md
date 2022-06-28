# Development

## Dependency

Arch/Manjaro:

```
# You need to install `yay` first since `fpm` is availabe in AUR
# Otherwise install `ruby` and follow Debian guide to install `fpm`
yay -Syu --noconfirm --needed base-devel git uboot-tools aarch64-linux-gnu-gcc cpio dpkg fpm docker multipath-tools
```

Debian/Ubuntu:

We use `docker` provided from distro's own repository. If you installed `docker` from another source, please remove `docker.io` from `apt install` command.

```
sudo apt update
sudo apt install -y build-essential bison flex libssl-dev python-is-python3 git u-boot-tools gcc-aarch64-linux-gnu cpio ruby multipath-tools docker.io
sudo gem install fpm
```

## Additional system config

```
sudo usermod -a -G docker $USER
sudo systemctl enable docker
sudo reboot
```
