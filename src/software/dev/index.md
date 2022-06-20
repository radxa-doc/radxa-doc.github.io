# Development

## Dependency

Arch/Manjaro:
```
sudo yay -Syu --noconfirm --needed base-devel git uboot-tools aarch64-linux-gnu-gcc cpio dpkg fpm docker multipath-tools
```

Debian/Ubuntu:
```
sudo apt update
sudo apt install -y build-essential git u-boot-tools gcc-aarch64-linux-gnu cpio ruby docker multipath-tools
sudo gem install fpm
```

## Additional system config
```
sudo usermod -a -G docker $UID
sudo systemctl enable docker
sudo reboot
```