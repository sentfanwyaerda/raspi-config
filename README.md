###raspi-config
- [original release](https://github.com/asb/raspi-config) ([release note](http://www.raspberrypilabs.com/raspi-config-the-new-cli-tool-raspbian/))
- more information on [elinux.org](http://elinux.org/RPi_raspi-config)

####add-on
- Hexxeh's [rpi-update](https://github.com/Hexxeh/rpi-update) -- firmware update method
- **[EXPERIMENTAL]** shrink rootfs -- To [shrink](http://www.howtoforge.com/linux_resizing_ext3_partitions) the SD-card to a bare minimum before backuping through *dd* or *Win32DiskImager*
- system upgrade -- updates and upgrades all installed programms
- raspi-config can update (back to) the originial *or* update this altered forked version
- semi-automated webserver configuration:
	- install and configure git
	- add a fixed ip-address to eth0:0
	- install apache, mysql, php, gd, geoip, ..
	- restore /var/www from a backup
	- setup backup method (cronjob /var/www to *.gz on external location)
	- patch apache to use *.conf in /var/www/domains/httpd.conf/

####Tested with
- Raspbian
- [Kali](http://kali.org/) (previous known as BackTrack)

####Easy install:
`` wget -O /sbin/raspi-config http://raw.github.com/sentfanwyaerda/raspi-config/master/raspi-config ``
You also might do this before, because the onboard clock ``date`` on the RaspberryPi says it's 1970.
`` apt-get install ntp fake-hwclock ``
