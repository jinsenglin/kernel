REF http://linux.vbird.org/linux_basic/0540kernel.php

# Prepare a building machine

```
vagrant init bento/centos-7.2 --box-version 2.3.1
vagrant up
vagrant ssh

sudo su
```

# Download a base kernel

```
wget https://cdn.kernel.org/pub/linux/kernel/v3.x/linux-3.10.tar.xz
```

# Unpack the base kernel and create /usr/src/linux directory

```
cd /usr/src
tar Jvxf /home/vagrant/linux-3.10.tar.xz
mv linux-3.10 linux 
```
