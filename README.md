# Unofficial iWave BSP Platform

This BSP helps build custom Linux distributions for the [iWave i.MX6 SODIMM SoM (iW-RainboW-G15M-SM)](https://www.iwavesystems.com/product/cpu-modules/sodimm-modules/i-mx6-sodimm-module-522/i-mx6-sodimm-module.html) with recent releases of the [Yocto Project](https://www.yoctoproject.org/).

The last official BSP release from iWave was compatible with Krogoth.

## Install Repo

To get the BSP you need to install [repo](https://gerrit.googlesource.com/git-repo/):

```sh
mkdir ~/bin
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
```

The above commands will download `repo` to `~/bin` and make it executable.

For more information about `repo`, see the [Repo Command Reference](https://source.android.com/setup/develop/repo). 

## Download the BSP

```sh
PATH=${PATH}:~/bin
mkdir ~/iwave-fslc-yocto
cd ~/iwave-fslc-yocto
repo init -u https://github.com/cpboyd/iwave-fslc-bsp.git -b thud
repo sync -j4
```

These commands will add `~/bin` to your path and use `repo` to download the BSP to `~/iwave-fslc-yocto`.

The source code for all included [layers](https://www.openembedded.org/Layers_FAQ) will be in `~/iwave-fslc-yocto/sources`.

## Build Examples

#### For a console-only image, you can build `core-image-base`:

```sh
MACHINE=imx6qdl-iwg15-sm DISTRO=fslc-framebuffer source ./setup-environment build_fb
bitbake core-image-base
```

The resulting build will be located in `~/iwave-fslc-yocto/build_fb`.

#### For an image with a GUI, you can build `fsl-image-gui` (or `fsl-image-qt5` to include the QT demos):

```sh
MACHINE=imx6qdl-iwg15-sm DISTRO=fslc-x11 source ./setup-environment build_x11
bitbake fsl-image-gui
```

The resulting build will be located in `~/iwave-fslc-yocto/build_x11`.
