#
# Copyright (C) 2007-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mpd
PKG_VERSION:=0.16
PKG_RELEASE:=6

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=@SF/musicpd
#PKG_MD5SUM:=824e1ce46c0f468865d9e5e403cdaf5d

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/mpd
  SECTION:=sound
  CATEGORY:=Sound
  TITLE:=Music Player Daemon
  URL:=http://www.musicpd.org/
# libvorbis and therewith libogg are needed for shout support
  DEPENDS:= \
	+BUILD_PATENTED:libmad \
	+glib2 +libcurl +libpthread +libffmpeg +libmms +libintl
endef

define Package/mpd/description
 MPD is a music player supporting flac, mp3 and ogg files. It is
 typically controlled over a network using one of it's many clients
 including mpc(console), gmpc(gnome), phpmp(php), etc...
endef

define Package/mpd/conffiles
/etc/mpd.conf
endef

# oggflac is not compatible with tremor
CONFIGURE_ARGS += \
	$(call autoconf_bool,CONFIG_BUILD_PATENTED,mad) \
	--disable-alsa \
	--disable-audiofile \
	--disable-mpc \
	--disable-lsr \
	--disable-ao \
	--disable-mvp \
	--disable-httpd-output 
	--disable-lame-encoder \
	--disable-vorbis-encoder \
	--disable-wave-encoder \
	--disable-inotify \
	--disable-un \
	--enable-ffmpeg \
	--disable-flac \
	--disable-vorbis \
	--disable-oggflac \
	--disable-cue \
	--disable-jack \
	--disable-modplug \
	--disable-pulse \
	--disable-sidplay \
	--disable-sqlite \
	--disable-shout \
	--disable-id3 \
	--disable-lastfm \
	--enable-mms \
	--enable-curl \
	--enable-oss \
	--disable-aac \
	--with-zeroconf=no \
	--disable-libOggFLACtest \
	--disable-test \
	--with-tremor=no \
	--with-faad=no \
	--disable-recorder-output \
	#--disable-largefile \
	--disable-httpd-output \

CONFIGURE_VARS += \
	$(if $(CONFIG_BUILD_PATENTED),MAD_CFLAGS="$(TARGET_CFLAGS)") \
	$(if $(CONFIG_BUILD_PATENTED),MAD_LIBS="$(TARGET_LDFLAGS) -lmad") \

TARGET_CFLAGS += \
	-std=gnu99 \
	-I$(STAGING_DIR)/usr/lib/libintl/include/ \
	-I$(STAGING_DIR)/usr/lib/libiconv/include/ \

TARGET_LDFLAGS += \
	-Wl,-rpath-link=$(STAGING_DIR)/usr/lib \
	-L$(STAGING_DIR)/usr/lib/libintl/lib/ \
	-L$(STAGING_DIR)/usr/lib/libiconv/lib/ \

# use gcc instead of g++ to avoid unnecessary linking against libstdc++
TARGET_CXX:=$(TARGET_CC)

define Package/mpd/install
	$(INSTALL_DIR) $(1)/etc
	$(CP) ./files/mpd.conf $(1)/etc/mpd.conf
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/mpd $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_DIR) $(1)/root/.mpd
	$(INSTALL_DIR) $(1)/root/music
	$(INSTALL_DIR) $(1)/root/.mpd/playlists
	$(INSTALL_BIN) ./files/mpd.init $(1)/etc/init.d/mpd
endef

$(eval $(call BuildPackage,mpd))
