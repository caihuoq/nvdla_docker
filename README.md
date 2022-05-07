# nvdla_docker
# pull images：
docker pull caihuoqing/nvdla-docker:v1.0
# run docker:
docker run -it  -v $your-mount-path:/workspace caihuoqing/nvdla-docker:v1.0 /bin/bash
# run nvdla simulator
  (based on qemu & tlm2.0)

./usr/local/nvdla/run-vp.sh
# rebuild linux image
if you want to use yourself linux image, 
Download the buildroot from https://buildroot.org/download.html
$ make qemu_aarch64_virt_defconfig
$ make menuconfig
* Target Options -> Target Architecture -> AArch64 (little endian)
* Target Options -> Target Architecture Variant -> cortex-A57
* Toolchain -> Custom kernel headers series -> 4.13.x
* Toolchain -> Toolchain type -> External toolchain
* Toolchain -> Toolchain -> Linaro AArch64 2018.05 
* Toolchain -> Toolchain origin -> Toolchain to be downloaded and installed
* Kernel -> () Kernel version -> 4.13.3
* Kernel -> Kernel configuration -> Use the architecture default configuration
* System configuration -> Enable root login with password -> Y
* System configuration -> Root password -> nvdla
* Target Packages -> Show packages that are also provided by busybox -> Y
* Target Packages -> Networking applications -> openssh -> Y

$make -j4

then you can backup buildroot/output/linux-xxx/.config
and replace buildroot/output/linux-xxx/ with your linux code

$make linux-rebuild

$make -j4
