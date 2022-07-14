# Building System Image

This documentation serves as a quick guide for building images for supported products. Custom images should refer to each build tool's reference for available options.

## Build with Radxa kernel and firmware

To get started, please first config your system according to [Development Reference](dev/index.md). This one will also include additional dependencies for building kernel and firmware in later steps.

You can then clone `rbuild` which is our image generator:

```shell
git clone --depth 1 https://github.com/radxa-repo/rbuild.git
cd rbuild
./rbuild
```

Running `rbuild` without any argument will display the help message, which lists the supported products, the supported distro, and flavors. You can then build the image with:

```shell
./rbuild <board> [distro] [flavor]
```

`distro` and `flavor` are optional arguments. If you omit them, a default value will be used.

Once the command returns, you can find the built image located in the same folder, along with the SHA-512 hash.

## Speed up image generation

Here are a few tricks to speed up image generation to make your debugging experience easier.

1. Update `common/rootfs.yaml` to use a faster APT mirrors.
2. Specify `-r` option when running `rbuild`. This will reuse the previously generated rootfs. Useful when you need to do frequent builds.
3. Specify `--no-compression` option when running `rbuild`. This will skip image compression, so `rbuild` can end sooner for you to flash the image.
4. While not strictly speeding up image generation, you can also specify `-s` option when running `rbuild`. This will shrink the image, so the empty space at the end of the image won't be written to the testing media, saving your time on flashing instead of building. This option does carry the caveat of requiring `sudo` to mount the image, which could block the building process depending on your setting.

## Build kernel from source

Once you are comfortable with `rbuild`, you can try with `lbuild` to create custom kernel for your image. Run the following commands to clone `lbuild` to your system:

```shell
git clone --depth 1 https://github.com/radxa-repo/lbuild.git
cd lbuild
./lbuild
```

Similarly running `lbuild` without any argument give you the help message. Supported forks are listed here as well. Running `./lbuild [fork]` to get the build going, and you can find the resulting deb packages in the same folder. There will be multiple `linux-images-....deb` packages. The one with the lartest size is the real kernel package, others are virtual packages.

However, to integrate kernel into the image, you should first check if the kernel is compatiable with your targeting product. A single kernel can support multiple products, and the list is defined as `SUPPORTED_BOARDS` in `forks/[fork]/fork.conf` file.

Once you have the correct kernel package, you can copy it to `rbuild` folder, and use `-k [linux-images.deb]` to specify a local kernel package in `rbuild`.

## Build firmware from source

In addition to custom kernel, you can also build custom firmware for your image. The most common choice is [U-Boot](https://github.com/u-boot/u-boot) but we are also looking to support [EDK2](https://github.com/tianocore/edk2) for EFI boot, hence we are calling this section "firmware" instead of the more commonly used "bootloader" in embedded development.

We have `ubuild` for building U-Boot, and at this point you should be pretty familiar with this family of tools:

```shell
git clone --depth 1 https://github.com/radxa-repo/ubuild.git
cd ubuild
./ubuild
```

The help message this time will show you the supported products. Unlike the kernel we have one firmware per product. This is to allow each firmware to have the correct hardware configuration coded in, as on ARM platform there is no standardized hardware discovery mechanism.

Simply running `./ubuild [product]` to have the U-Boot package built. Copy it to `rbuild` folder and use `-f [u-boot.deb]` to specify a local firmware package in `rbuild`.
