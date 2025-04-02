# Setting up a Kernel Dev Environment using QEMU

I will make two guides. First one is minimal and faster. Second one gonna be more specific and "stable".

NOTE: I am doing this from Arch Linux, so commands may differ if you are using other distros and especially packet managers.


## Fast approach

- Get dependencies for compiling kernel
- Get your favourite linux kernel version as a git from https://www.kernel.org/
- Then open the folder and execute:

```$ make defconfig```
```$ make -j$(nproc)```

- Then Generate an Initramfs in a folder of your choice (I'll call it INITRAM_FOLDER):

```$ mkinitcpio -g INITRAM_FOLDER/ramdisk.img```

- Then you are free to start QEMU:

``` 
$  qemu-system-x86_64 \
  -kernel KERNEL_FOLDER/arch/x86_64/boot/bzImage \
  -nographic \
  -append "console=ttyS0" \
  -initrd INITRAM_FOLDER/ramdisk.img \
  -m 1G \
  --enable-kvm \
  -cpu host \
  -s -S &
```
