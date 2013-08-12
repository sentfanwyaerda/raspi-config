###raspi-config
- [original release](https://github.com/asb/raspi-config) ([release note](http://www.raspberrypilabs.com/raspi-config-the-new-cli-tool-raspbian/))
- more information on [elinux.org](http://elinux.org/RPi_raspi-config)

####add-on
*Adding some more voodoo to my RaspberryPi* and being able to do a quick complete rebuild after datacorruption of the SD-card, or switch of distribution.
- Hexxeh's [rpi-update](https://github.com/Hexxeh/rpi-update) -- firmware update method
- **[EXPERIMENTAL]** shrink rootfs -- To [shrink](http://www.howtoforge.com/linux_resizing_ext3_partitions) the SD-card to a bare minimum before backuping through *dd* or *Win32DiskImager*
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

####Tested with:
- Raspbian
- [Kali](http://kali.org/) (previous known as BackTrack)

####Easy install:
*(if not already available through the RaspberryPi flavoured Linux distrubution you use)*
``` wget -O /sbin/raspi-config http://raw.github.com/sentfanwyaerda/raspi-config/master/raspi-config && chmod +x /sbin/raspi-config ```

- In case your onboard clock of the RaspberryPi says it's 1970 (when you use ``date`` ): ``apt-get install ntp fake-hwclock && ntpdate -q ntp.ubuntu.com``.
- In case you run into dependency errors: ``apt-get install ntp fake-hwclock bc git-core`` and ``update-rc.d cron enable``
