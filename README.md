REF1 http://linux.vbird.org/linux_basic/0540kernel.php

REF2 https://medium.freecodecamp.org/building-and-installing-the-latest-linux-kernel-from-source-6d8df5345980

REF3 https://linode.com/docs/tools-reference/custom-kernels-distros/custom-compiled-kernel-centos-7/

REF4 https://www.howtoforge.com/kernel_compilation_centos

# Prepare a building machine

```
vagrant init bento/centos-7.2 --box-version 2.3.1
vagrant up
vagrant ssh

sudo su
yum install -y ncurses-devel bc
yum group install -y "Development Tools"
```

# Download a base kernel

```
wget https://cdn.kernel.org/pub/linux/kernel/v3.x/linux-3.10.tar.xz
```

# Unpack the base kernel

```
tar -Jxvf linux-3.10.tar.xz -C /usr/src/kernels/
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

# Hint lazy way is `cp /boot/config-3.10.0-327.el7.x86_64 /usr/src/kernels/linux-3.10/.config`
```

# Compile the base kernel source code

```
make -j 8
ls arch/x86/boot/bzImage
```
# Install the new custom kernel modules

```
make modules_install -j 8
ls /lib/modules/3.10.0
```

# Install the new custom kernel

```

# OR
make install -j 8
ls /boot/System.map-3.10.0
ls /boot/vmlinuz-3.10.0
ls /boot/initramfs-3.10.0.img
```

# Create the Initial Ram Disk (initrd)

```
dracut -v /boot/initramfs-3.10.0.img 3.10.0

# OR
# update-initramfs -c -k 3.10.0
```

# Update the boot loader menu

```
# TBD
# grub2-mkconfig -o /boot/grub2/grub.cfg

# OR
# update-grub
```

# Verify the new custom kernel by rebooting this building machine


