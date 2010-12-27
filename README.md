 ---------------------------------------------------
   OpenWRT Radio Project v 0.5
	MPD 0.16 (ACC,WMA,MP3, Shoutcast)
	One button operation (play, next, stop)
	Web UI
	USB Storage (FAT32, NTFS, ext3)
	UPNP Dlna
 ---------------------------------------------------

How to compile:
 - Prepare your compile enviroment - > http://wiki.openwrt.org/doc/howto/build
 - Clone original OpenWRT backfire branch
 - Update package feeds
 - Clone this repository
 - Compile
 - Upload to router (set it to failsafe mode first)

Run following:
    mkdir OpenWRTradio && cd OpenWRTradio && svn co svn://svn.openwrt.org/openwrt/trunk/
    ./scripts/feeds update -a
    git clone git://github.com/dz0ny/OpenWRT-internet-radio.git .
    make prereq && make
    atftp --trace --option "timeout 1" --option "mode octet" --put --local-file bin/brcm-2.4/openwrt-brcm-2.4-squashfs.trx 192.168.1.1

Remarks:
 - Edit packages/base-files/files/etc/init.d/radio (set initial radios to load)
 - Edit packages/base-files/files/etc/init.d/first (wlan to connect to and timezone)
 - Edit packages/base-files/files/etc/crontabs/root (Alarm radio clock...)
