REF https://linode.com/docs/tools-reference/custom-kernels-distros/custom-compiled-kernel-centos-7/

Addtional Resources

* http://linux.vbird.org/linux_basic/0540kernel.php
* https://medium.freecodecamp.org/building-and-installing-the-latest-linux-kernel-from-source-6d8df5345980
* https://www.howtoforge.com/kernel_compilation_centos
* http://connecttech.com/resource-center/kdb271-making-sense-linux-release-numbers-kernel-revisions/

# Prepare a building machine

NOTE: DON'T USE VAGRANT

```
# boot virtualbox machine with disc http://archive.kernel.org/centos-vault/7.2.1511/isos/x86_64/CentOS-7-x86_64-Minimal-1511.iso

# activate connections
nmtui

yum install -y wget ncurses-devel bc
yum group install -y "Development Tools"
```

# Download a base kernel

```
cd /usr/src
wget https://cdn.kernel.org/pub/linux/kernel/v3.x/linux-3.10.tar.xz
wget https://cdn.kernel.org/pub/linux/kernel/v3.x/linux-3.10.1.tar.xz
```

# Unpack the base kernel

```
tar -xvf linux-3.10.tar.xz
cd linux-3.10

# OR
# tar -Jxvf linux-3.10.tar.xz -C /usr/src/kernels/
```

# Clean the base kernel source code

```
cd /usr/src/kernels/linux-3.10/
make mrproper
```

# Prepare .config file

```
touch .config
make menuconfig

# Hint lazy way is `cp /boot/config-3.10.0-327.el7.x86_64 .config && make oldconfig`
```

# Compile the base kernel source code

```
make -j 8
ls arch/x86/boot/bzImage
```
# Install the new custom kernel modules

```
rm -rf /lib/modules/3.10.0

make modules_install -j 8
ls /lib/modules/3.10.0
```

# Install the new custom kernel

```
rm -rf /boot/*

make install -j 8
ls /boot/System.map
ls /boot/System.map-3.10.0
ls /boot/vmlinuz
ls /boot/vmlinuz-3.10.0
ls /boot/initramfs-3.10.0.img
```

# Create the Initial Ram Disk (initrd)

```
mkinitrd /boot/initrd-3.10.0.img 3.10.0 # will use 1. dracut command 2. /lib/modules/3.10.0/ dir
ls /boot/initrd-3.10.0.img

# OR
# dracut -v /boot/initramfs-3.10.0.img 3.10.0

# OR
# update-initramfs -c -k 3.10.0
```

# Update the boot loader menu

```
grub2-mkconfig -o /boot/grub2/grub.cfg

# OR
# update-grub
```

# Verify the new custom kernel by rebooting this building machine


