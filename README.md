REF http://linux.vbird.org/linux_basic/0540kernel.php

# Prepare a building machine

```
vagrant init bento/centos-7.2 --box-version 2.3.1
vagrant up
vagrant ssh

sudo su
yum install -y ncurses-devel
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
make -j 4 clean bzImage modules
ls arch/x86/boot/bzImage
```
# Install the new custom kernel

```
# TBD
# cp arch/x86/boot/bzImage /boot/vmlinuz-3.10.89vbird
# cp .config /boot/config-3.10.89vbird
# chmod a+x /boot/vmlinuz-3.10.89vbird
# cp System.map /boot/System.map-3.10.89vbird
# gzip -c Module.symvers > /boot/symvers-3.10.89vbird.gz
# restorecon -Rv /boot
```

# Install the new custom kernel modules

```
make modules_install
ls /lib/modules/
```

# Create the Initial Ram Disk (initrd)

```
dracut -v /boot/initramfs-3.10.img 3.10
```

# Update the boot loader menu

```
# TBD
# grub2-mkconfig -o /boot/grub2/grub.cfg
```

# Verify the new custom kernel by rebooting this building machine


