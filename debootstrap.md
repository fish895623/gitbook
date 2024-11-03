# debootstrap


## Install Tools 

```sh
sudo apt update
sudo apt install debootstrap arch-install-scripts
```

## format disk

- gdisk
- fdisk

any things you like.

I will use fdisk

results:

```sh
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Device does not contain a recognized partition table.
Created a new DOS (MBR) disklabel with disk identifier 0xc4dcbe2d.

Command (m for help): g

Created a new GPT disklabel (GUID: 444AA2A4-54E9-4C17-81E4-D8164F5665FF).

Command (m for help): n
Partition number (1-128, default 1):
First sector (2048-266338270, default 2048):
Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-266338270, default 266336255): +512M

Created a new partition 1 of type 'Linux filesystem' and of size 512 MiB.

Command (m for help): n
Partition number (2-128, default 2):
First sector (1050624-266338270, default 1050624):
Last sector, +/-sectors or +/-size{K,M,G,T,P} (1050624-266338270, default 266336255):

Created a new partition 2 of type 'Linux filesystem' and of size 126.5 GiB.

Command (m for help): w
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.
```

Create File Systems

```
mkfs.vfat -F32 /dev/sda1
mkfs.ext4 -j /dev/sda2
```

Mount on /mnt folder

```sh
mount /dev/sda2 /mnt
mkdir -p /mnt/boot/efi
mount /dev/sda1 /mnt/boot/efi
```

Install base system using debootstrap.

```
debootstrap __version__ /mnt https://archive.ubuntu.com/ubuntu
```

Update /mnt/etc/apt/sources.list

```
deb https://mirror.kakao.com/ubuntu noble main restricted universe multiverse
deb https://mirror.kakao.com/ubuntu noble-security main restricted universe multiverse
deb https://mirror.kakao.com/ubuntu noble-updates main restricted universe multiverse
```

Generate fstab

genfstab is in `arch-install-scripts` packages

```
genfstab /mnt > /mnt/etc/fstab
```


Chroot /mnt

genfstab is in `arch-install-scripts` packages

```
arch-chroot /mnt
```

Install necessary packages

```
apt update
apt upgrade
apt install --no-install-recommends \
  linux-{,image-,headers-}generic \
  linux-firmware initramfs-tools efibootmgr neovim build-essential
```

Set time

If you want to use ncurse to configure timezone, `dpkg-reconfigure tzdata`.

configure with script, `echo __TIMEZONE__ > /etc/timezone && dpkg-reconfigure -f noninteractive tzdata`

Set locale

Tui to configure locales, `dpkg-reconfigure locales`

Scripts to configure locales

```
sed -i 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/g' /etc/locale.gen
echo 'LANG=en_US.UTF-8' > /etc/default/locale
locale-gen
```

## Create User

### Root Password

`passwd`

### Create User

Create sudo user

```sh
useradd -mG sudo __username__
passwd __username__
```

## Network

`/etc/systemd/network/ethernet.network`
```ini
[Match]
Name=eth0 # Replace device name using ip addr

[Network]
DHCP=yes
```

### Register service.

`systemctl enable systemd-networkd`

## Install bootloader

```
apt install grub2 grub-efi-amd64
```

`grub-install /dev/sda --efi-directory=/boot/efi`

Result:
```
Installing for x86_64-efi platform.
Installation finished. No error reported.
```
