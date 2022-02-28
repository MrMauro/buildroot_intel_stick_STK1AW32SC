# The problem

My purpose is to generate an image based on buildroot 2021.11.1 that can be flashed on the internal eMMC of the Intel Stick STK1AW32SC, which is based on Intel Atom x5-Z8300

A vanilla image (using the default buildroot pc_x86_64_efi_defconfig) correctly boots from USB.
However the /dev/mmcblk* related to the eMMC don't appear. That is expected has the vanilla kernel does not have the MMC modules built in.

# Initial attempt

To do it, I used the BR2_LINUX_KERNEL_CONFIG_FRAGMENT_FILES to append a linux.fragment enabling the CONFIG_MMC and other related.

- This is the .config used:
https://github.com/MrMauro/buildroot_intel_stick_STK1AW32SC/blob/f0abe726d5648499f94bf9d96e4d5eb9745447a4/external_is/configs/intelstick_defconfig

- And this is the linux.fragment file used:
https://github.com/MrMauro/buildroot_intel_stick_STK1AW32SC/blob/f0abe726d5648499f94bf9d96e4d5eb9745447a4/external_is/board/pc/intelstick/linux.fragment

Again, booting with the resulting image written on the USB works ok.

Result:
- Still ls \dev\m* does not show the expected mmcblk* folders.

# 2nd attempt

I decided to include on the kernel other 'drivers' related to the MMC, as a kernel.

- New linux.fragment file used:
https://github.com/MrMauro/buildroot_intel_stick_STK1AW32SC/blob/bb4c7faba4f2b0e45907b544e1762c5b9525ee72/external_is/board/pc/intelstick/linux.fragment

Result:
- No /dev/mmcblk* folders.
- lsmod shows about 4 modules, none of them seem to be related to the MMC drivers.