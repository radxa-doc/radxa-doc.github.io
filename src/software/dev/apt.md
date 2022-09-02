# apt

Our apt repo automatically source the release binaries from `radxa-pkg` organization. We have the following convention to ensure the package info can be parsed by our tools.

1. Release's name has to be a version number only.

   `apt-repo-action` will record the release name as version number and store it in [`pkgs.json`](https://github.com/radxa-repo/apt/blob/gh-pages/pkgs.json). If the release name contains additional info, that might break future package gathering operation.

2. Split unrealated packages into their own repo.

    `apt-repo-action` only compare the latest release with `pkgs.json`. As such if two packages are upgraded independently, they should be split into 2 different repo, so their content can be updated only when needed.

    However, if the same source code will generate multiple packages, they can be put in the same repo and the same release, so everything can be updated together.

3. Use `pkg.conf` to customize package upload.

    By default, every package will be uploaded to [`bullseye` and `jammy`](https://github.com/radxa-repo/apt/blob/gh-pages/.apt-repo.json) release. If you want to adjust the release destination, you can add a `pkg.conf` file in your release assets.

    It will have the following format with comment added. Note this has to be a legal json document and comment is actually not supported in the spec:

    ```json
    {
        // Full file name
        "sample_1.0-1_all.deb": {
            // List targeting releases
            "Releases": [
                "bullseye",
                "jammy"
                // The last item in the array cannot have trailing comma!
            ]
        },
        "rockchip_1.0-1_all.deb": {
            // Upload to vendor specific release
            "Releases": [
                "bullseye-rockchip"
            ]
        },
        "private_1.0-1_all.deb": {
            // Do not upload this package
            "Releases": []
        }
    }
    ```

    Currently every releases share the same binary pool, so package with exact same file name will be overwritten by one another.