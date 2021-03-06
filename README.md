###raspi-config
- [original release](https://github.com/asb/raspi-config) ([release note](http://www.raspberrypilabs.com/raspi-config-the-new-cli-tool-raspbian/))
- more information on [elinux.org](http://elinux.org/RPi_raspi-config)

####add-on
*Adding some more voodoo to my RaspberryPi* and being able to do a quick complete rebuild after datacorruption of the SD-card, or switch of distribution.
- Hexxeh's [rpi-update](https://github.com/Hexxeh/rpi-update) -- firmware update method
- ~~shrink rootfs &mdash; To [shrink](http://www.howtoforge.com/linux_resizing_ext3_partitions) the SD-card to a bare minimum before backuping through *dd* or *Win32DiskImager*~~
	- Use ``zerofill`` instead. It fills the sd-card with a single file of zero's (which will be automatically deleted through the ``rc.local``-patch). On your desktop with cardreader (``sdcard=/dev/sdb && ``): ``dd if=$sdcard | gzip > rpi-$(date +%F).gz`` and restore with: ``gzip -dc rpi-$(date +%F).gz | dd of=$sdcard``
- system upgrade -- updates and upgrades all installed programms
- raspi-config can update (back to) the originial *or* update this altered forked version
- semi-automated webserver configuration:
	- install and configure git
	- add a fixed ip-address to eth0:0
	- ~~install apache, mysql, php, gd, geoip, ..~~
	- ~~restore /var/www from a backup~~
	- setup backup method ``backup-www`` (cronjob /var/www to /var/backups/*.gz, ``get-backup-www`` gets it from smb://$ip/backups/)
	- patch apache to use *.conf in /var/www/domains/httpd.conf/
	- patch samba to enable smb://$ip/www/ *(rw)* and smb://$ip/backups/ *(r)*
- expand_ro_rootfs &mdash; Works similair to expand_rootfs, but makes ``/`` **readonly** and adds ``/home``-partition with a set of symbolic links from ``/etc/fstab``, ``/var/www/`` and ``/var/backups/``. With the tools: ``freeze_rootfs``, ``unfreeze_rootfs``, ``backup_rootfs``, ``restore_rootfs``. WHY? Because this is one of the methods to limit data corruption of the SD-card, and adds a extra level of security to your system.
- install GPIO and Python
- [toolset](./toolset.md)
- wifi configuration (patched from [mikerr](https://github.com/mikerr/raspi-config))

####Tested with:
- Raspbian
- [Kali](http://kali.org/) (previous known as BackTrack)

####Easy install:
*(if not already available through the RaspberryPi flavoured Linux distrubution you use)*
``` wget -O /sbin/raspi-config http://raw.github.com/sentfanwyaerda/raspi-config/master/raspi-config && chmod +x /sbin/raspi-config ```

- In case your onboard clock of the RaspberryPi says it's 1970 (when you use ``date`` ): ``apt-get install fake-hwclock ntp ntpdate ca-certificates && ntpdate -u ntp.ubuntu.com``.
- In case you run into dependency errors, also run: ``apt-get install lua bc git-core`` and ``update-rc.d cron enable``
