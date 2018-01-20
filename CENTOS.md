REF https://wiki.centos.org/HowTos/Custom_Kernel

# Prepare a building machine

```
# wget http://archive.kernel.org/centos-vault/7.2.1511/isos/x86_64/CentOS-7-x86_64-Minimal-1511.iso
# virutalbox boot a machine with the distro
```

# Download the source code

```
[user@host]$ rpm -i http://vault.centos.org/7.2.1511/updates/Source/SPackages/kernel-3.10.0-327.3.1.el7.src.rpm 2>&1 | grep -v exist
```

WIP
