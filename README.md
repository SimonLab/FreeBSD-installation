# FreeBSD Installation Process

Following along: https://www.youtube.com/watch?v=vXP1qt77aYE&list=PL49DYk6kw0EIAAP7-KOhsHYhFDLMh1oRO&index=16

## Create FreeBSD image

### Download

The current release version are ...
Select the download file depending on how you install FreeBSD.
We are using a usb key and the laptop we are install on is a Thinkpad x230 so
we want to install the architecture amd64 with memstick.

TODO: 
- explain current version 11, 12, and 13
- explain architecture amd64
- add link to page


### Create usb boot image

use the dd command or on Ubuntu you can use the disk checker

TODO: explain dd command

## Start and Install FreeBSD 

Plug the usb key and select the image on start.
On the Thinkpad x230 press the F12 key on start,
you should then be able to select the usb key:


TODO: add image of boot screen

After 10 seconds the default `install` option is selected.

- Select  keyboard
- Enter the hostname for the computer (ie the name on the network)
- Select optional system components
  - [ ] base-dbg
  - [ ] kernel-dbg
  - [ ] lib32-dbg
  - [x] lib32
  - [x] ports
  - [x] src
  - [ ] tests

- Select how to partition disk
  - [x] Auto UFS
  - [ ] Manual
  - [ ] Shell
  - [ ] Auto ZFS

Select the disk and choose the format entire disk.

- Select partition scheme
  - [ ] Apple Partition Map
  - [ ] BSD Labels
  - [x] GUID Partition Table
  - [ ] DOS Partitions
  - [ ] Sun VT0C8 Partition Table

TODO: what are the optional components system; What are the type of partition; what are partition scheme

- Define root password
- Configure Network. Select the wifi card. For the x230 Intel Centrino Advanced-N 6205
  - Select regdomain: https://forums.freebsd.org/threads/what-is-the-correct-regdomain-code.60469/
    - ETSI and GB United Kingdom
    - configure ipv4 and use DHCP

- Select time zone: Europe/UK

- Select services to start at boot
  - [ ] local_unbound
  - [x] sshd
  - [x] moused
  - [x] ntpdate
  - [ ] powerd
  - [ ] dumpdev

- Select system security: Select all

- Add user account
  - add user to wheel group to be able to use `su` to login as root

- Apply, exit installer and reboot

### Update

With FreeBSD the base system and the userland is seperated.
Update the system with `freebsd-update fetch` then `freebsd-update install`

- restart with `shutdown -r now`
- you can also use `pkg update`

## Install xfce Desktop environment
ref: https://www.youtube.com/watch?v=BgrcwCJA2lU

- install xorg: `pkg install xorg` implementation of X Window System
- install xfce: `pkg install xfce` desktop environment
- install  sddm `pgk install sddm` display/login manager

- edit /etc/rc.conf and add:

 ```
dbus_enable="YES" # https://en.wikipedia.org/wiki/D-Bus
hald_enable="YES" # hardware abstraction layer https://en.wikipedia.org/wiki/Hardware_abstraction
sddm_enable="YES"


edit/create the .xinitrc on the user home directory and add, see https://www.freebsd.org/doc/handbook/x11-wm.html

```
exec startxfce4
```

Reboot: `su` then `shutdown -r now` and you should be able to login into xfce.

