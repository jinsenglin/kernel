REF http://linux.vbird.org/linux_basic/0540kernel.php

# Prepare a building machine

```
vagrant init bento/centos-7.2 --box-version 2.3.1
vagrant up
vagrant ssh

sudo su
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

# Hint lazy way is `cp /boot/config-3.10.0-327.el7.x86_64 /usr/src/kernels/3.10/.config`
```

# 
