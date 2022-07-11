# pkgbase

`pkgbase` contains a set of helper scripts to help you create `radxa-repo` packages. The focus here is to simplify common package generation tasks, while enforcing some policies on all our packages.

A very basic package file can be seen here (`pkg.conf.shell`), which actually creates nothing:

```bash
PB_PKGS=( "shell" )

shell_package() {
    echo "Shell package can build in ways you like."
}
```

`pkg.conf` supports building multiple packages. Simply add the build prefix to `PB_PKGS` array, and write the mandatory `prefix_package` function for each package.

`pkgbase` also provides multiple hooks for advanced builds.

## Create new package

To create new package, simply base your `main` branch off `root` branch from this repo:

```bash
PKG_NAME="my-new-package"
mkdir $PKG_NAME
cd $PKG_NAME
git init
git remote add upstream https://github.com/radxa-repo/pkgbase.git
git fetch upstream
git checkout -b main upstream/root
git remote add origin https://github.com/radxa-pkg/$PKG_NAME.git
git push -u origin main
```

You can then add `pkg.conf` file to the repo. `pkgbase` provides some sample `pkg.conf` file for you to use as a starting point. Currently the following types of package are supported:

- [fpm]() that packages an existing root folder structure (usually `./root` folder) into a deb file. Requires `PB_MODULES=( "fpm" )` for loading `fpm` module.
- [shell]() that allows abritary build scripts.

## Build package

Run the following command:

```
PKG_NAME="my-new-package"
git clone --depth 1 https://github.com/radxa-repo/pkgbase.git
git clone --depth 1 https://github.com/radxa-pkg/$PKG_NAME.git
cd $PKG_NAME
../pkgbase/build.sh pkg.conf
```

You can check `.mod` files to see some additional dependencies each module requires. This is currently designed for GitHub Actions so that is not a complete list.

