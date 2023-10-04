# Install LXC on Ubuntu 22.04|20.04|18.04|16.04

## Introduction of lxc

LXC is a lightweight Virtualization technology,
that is used to run multiple isolated virtual units,
often referred to as containers in a chroot environment,
on a single host using a single Linux kernel.

- we will do installation with help of upstreame repository using command:

```bash
sudo apt update
sudo apt install lxc
```

- After the installation, define uid mappings to run containers as non root user

```bash
#  Create directory if it doesn't exist
mkdir -p ~/.config/lxc

# Add configs required
echo "lxc.include = /etc/lxc/default.conf" > ~/.config/lxc/default.conf
echo "lxc.idmap = u 0 100000 65536" >> ~/.config/lxc/default.conf
echo "lxc.idmap = g 0 100000 65536" >> ~/.config/lxc/default.conf
echo "lxc.net.0.type = veth" >> ~/.config/lxc/default.conf
echo "lxc.net.0.link = lxcbr0" >> ~/.config/lxc/default.conf
echo "lxc.net.0.link = lxcbr0" >> ~/.config/lxc/default.conf
echo "$USER veth lxcbr0 2" | sudo tee -a /etc/lxc/lxc-usernet
```

- check all available config file using below command:

```bash
lxc-config -l
lxc.default_config
lxc.lxcpath
lxc.bdev.lvm.vg
lxc.bdev.lvm.thin_pool
lxc.bdev.zfs.root
lxc.cgroup.use
lxc.cgroup.pattern
```

## Create lxc container

```bash
lxc-create -t download \
  -n mylxc-ubuntu -- \
  --dist ubuntu \
  --release focal \
  --arch amd64
```

> Where:

- **-n** for the name of the container
- **-t** for a template.

## OR

> If you get an error message “ERROR: Unable to fetch GPG key from keyserver“,
you can use **--no-validate** option:

```bash
lxc-create -t download \
  -n mylxc-ubuntu -- \
  --dist ubuntu \
  --release focal \
  --arch amd64 \
  --no-validate
```

- As we have craeted our first lxc container we will list from below command :

```bash
lxc-ls
```

- To start the container

```bash
lxc-start -n <container-name>

like:
lxc-start -n lxc-ubuntu
```

## Some usefull command for lxc

```bash
lxc-info <container-name>
lxc-ls
lxc attach <conatiner name>
lxc-destroy <container name>
```
