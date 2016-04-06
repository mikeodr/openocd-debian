openocd-debian
================

Debian packaging files for [openocd](http://openocd.org/).
If you just want to access the resultant debs, please see the
[launchpad PPA](https://launchpad.net/~clearpath-robotics/+archive/ubuntu/stm32).


Publishing to Launchpad
-----------------------

Better instructions coming soon, but in short:

 - Create a workspace directory.

 - Set an env var with the version you are releasing:
    ```
    VER=0.9.0
    ```

 - Clone this repo to a path like `openocd-x.y.z`:
    ```
    git clone https://github.com/mikeodr/openocd-debian openocd-$VER
    ```

 - Download the [openocd source tarball](https://sourceforge.net/projects/openocd/files/openocd/)
   for the version to release, and extract it, overwriting the files from this repo:
    ```
    wget http://downloads.sourceforge.net/project/openocd/openocd/$VER/openocd-$VER.tar.bz2 -O openocd_$VER.orig.tar.gz
    tar xvjf openocd_$VER.orig.tar.gz
    ```

 - Now inside the workspace/openocd-x.y.z/debian folder:

   * run `dch`, and edit the changelog accordingly.
   * run `generate` to create the templated rules file.

 - In the openocd-x.y.z folder, build the source package, and upload it to the PPA:
    ```
    debuild -S
    dput ppa:clearpath-robotics/stm32
    ```

To run a local build, instead do:

    debuild -uc -us

When complete, commit your changes back to this repo:

    git checkout .gitignore README.md
    git add .
    git commit -m "Changes for $VER"
