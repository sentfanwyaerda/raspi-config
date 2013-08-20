raspi-config++ Kali Tools
=========================
*Note: in the examples below '2013-07-31' equals now.*

#### ``rc.local`` patch
This is my own ``rc.local``, which (re)starts several services (apache, mysql, ntp, samba), adds a fixed ip adress and wifi, removes */var/zero.txt* and forces the RPi to do a ``fsck`` every boot.

#### ``lnmv from to``
Just a nifty tool to ``mv $1 $2 && ln -s $2 $1`` (move and backlink).

### for */var/www*
#### ``backup-www``
It creates a datestamped tar.gz-ball (with md5 file) in */var/backups* containing all data within */var/www*. Will be renamed to an alias of: ``backup-home /var/www``

#### ``backup-home [directory]``
#### ``restore-home [directory] [date=2013-07-31]``

#### ``get-backup-www ip user password [date=2013-07-31] [extension=tgz]``
It gets your most recent, or desired, backup from the samba server on **ip** (``smb://$user:$password@$ip/backups/www\[$date\].$extension``). 

### for *rootfs*
#### ``zerofill [size] [file=/var/zero.txt] [device=/dev/zero]``
It creates the file */var/zero.txt* to be completely filled with zero's. When (while reading out your sdcard on your desktop) creating a backup, all junk data is replaced with the emptyness of this file, while doing so it optimizes for best compression.

#### ``freeze-rootfs``
It updates the */etc/fstab* to make the *rootfs* **READ ONLY**. This to limit the possibility of getting data corruption or un-authorized system modifications.

#### ``unfreeze-rootfs``
It turns the *rootfs* back to being **READ WRITE**, so you can do installations and updates.

#### ``backup-rootfs``
It creates a complete backup of the *rootfs* (without the */home*, */var/backups* and */var/www*)