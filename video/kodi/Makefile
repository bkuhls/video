#
# Copyright (C) 2017  Stijn Tintel <stijn@linux-ipv6.be>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=kodi
PKG_CODENAME:=Matrix
PKG_VERSION:=19.1
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://github.com/xbmc/xbmc/archive/$(PKG_VERSION)-$(PKG_CODENAME)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_CODENAME).tar.gz
PKG_HASH:=195a916a32057e259e6f42b49ba8f07cc6253460018851a52deb058ae938c58c

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)-$(PKG_CODENAME)

PKG_LICENSE:=GPL-2
PKG_LICENSE_FILES:=LICENSE.GPL

PKG_BUILD_DEPENDS:=flatbuffers/host kodi-jsonschemabuilder/host kodi-texturepacker/host spdlog
PKG_BUILD_PARALLEL:=1
PKG_CHECK_FORMAT_SECURITY:=0
CMAKE_BINARY_SUBDIR:=openwrt-build

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk
$(call include_mk, python-package.mk)

TAR_OPTIONS:=--strip-components 1 $(TAR_OPTIONS)
TAR_CMD=$(HOST_TAR) -C $(1) $(TAR_OPTIONS)

define Package/kodi/Default
  URL:=https://kodi.org/
  MAINTAINER:=Stijn Tintel <stijn@linux-ipv6.be>
endef

define Package/kodi
  $(call Package/kodi/Default)
  SECTION:=multimedia
  CATEGORY:=Multimedia
  TITLE:=kodi
  USERID:=kodi=9777:kodi=9777
  DEPENDS:= \
	@TARGET_x86 \
	+TARGET_x86:mesa \
	+alsa-lib \
	+PACKAGE_bluez-libs:bluez-libs \
	+flatbuffers \
	+fontconfig \
	+fribidi \
	+fstrcmp \
	+giflib \
	+libass \
	+PACKAGE_libcap:libcap \
	+libcdio \
	+libcdiopp \
	+libcec \
	+libcrossguid \
	+libcurl \
	+libffmpeg-full \
	+libfmt \
	+libfreetype \
	+libiconv-full \
	+libinput \
	+libjpeg \
	+liblzo \
	+PACKAGE_libmicrohttpd-no-ssl:libmicrohttpd-no-ssl \
	+PACKAGE_libmicrohttpd-ssl:libmicrohttpd-ssl \
	+libopenssl \
	+libpcre \
	+libpcrecpp \
	+libplist \
	+libpng \
	+libsqlite3 \
	+libstdcpp \
	+libudev-zero \
	+PACKAGE_libupnp:libupnp \
	+libuuid \
	+PACKAGE_libva:libva \
	+libx264 \
	+libxkbcommon \
	+libxml2 \
	+PACKAGE_libxslt:libxslt \
	+PACKAGE_pulseaudio:pulseaudio \
	+python3 \
	+python3-codecs-src \
	+python3-ctypes-src \
	+python3-email-src \
	+python3-logging-src \
	+python3-sqlite3-src \
	+python3-urllib3 \
	+rapidjson \
	+PACKAGE_shairplay:shairplay \
	+taglib \
	+tinyxml
endef

define Package/kodi/description
Kodi Home Theater Software
endef

CMAKE_OPTIONS += \
	-DENABLE_APP_AUTONAME=OFF \
	-DAPP_RENDER_SYSTEM=gles \
	-DCORE_PLATFORM_NAME=gbm \
	-DENABLE_ALSA=ON \
	-DENABLE_AIRTUNES=$(if $(CONFIG_PACKAGE_shairplay),ON,OFF) \
	-DENABLE_AVAHI=OFF \
	-DENABLE_BLUETOOTH=$(if $(CONFIG_PACKAGE_bluez-libs),ON,OFF) \
	-DENABLE_BLURAY=OFF \
	-DENABLE_CAP=$(if $(CONFIG_PACKAGE_libcap),ON,OFF) \
	-DENABLE_CCACHE=$(if $(CONFIG_CCACHE),YES,NO) \
	-DENABLE_CEC=ON \
	-DENABLE_DBUS=OFF \
	-DENABLE_DVDCSS=ON \
	-DENABLE_EVENTCLIENTS=ON \
	-DENABLE_INTERNAL_CROSSGUID=OFF \
	-DWITH_FFMPEG=$(STAGING_DIR)/usr \
	-DFLATBUFFERS_FLATC_EXECUTABLE=$(STAGING_DIR_HOSTPKG)/bin/flatc \
	-DENABLE_LDGOLD=OFF \
	-DENABLE_MICROHTTPD=$(if $(CONFIG_PACKAGE_libmicrohttpd-no-ssl)$(CONFIG_PACKAGE_libmicrohttpd-ssl),ON,OFF) \
	-DENABLE_MYSQLCLIENT=OFF \
	-DENABLE_NFS=OFF \
	-DENABLE_OPTICAL=OFF \
	-DENABLE_PLIST=ON \
	-DENABLE_PULSEAUDIO=$(if $(CONFIG_PACKAGE_pulseaudio),ON,OFF) \
	-DENABLE_SMBCLIENT=OFF \
	-DENABLE_TESTING=OFF \
	-DENABLE_UDEV=ON \
	-DENABLE_UPNP=$(if $(CONFIG_PACKAGE_libupnp),ON,OFF) \
	-DENABLE_VAAPI=$(if $(CONFIG_PACKAGE_libva),ON,OFF) \
	-DENABLE_VDPAU=OFF \
	-DENABLE_XSLT=$(if $(CONFIG_PACKAGE_libxslt),ON,OFF) \
	-DWITH_TEXTUREPACKER="$(STAGING_DIR_HOSTPKG)/bin/TexturePacker" \
	-DWITH_JSONSCHEMABUILDER="$(STAGING_DIR_HOSTPKG)/bin/JsonSchemaBuilder"

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/kodi $(1)/usr/share/kodi
	$(CP) $(PKG_INSTALL_DIR)/usr/include/kodi/*.h $(1)/usr/include/kodi
	$(CP) $(PKG_INSTALL_DIR)/usr/share/kodi/cmake $(1)/usr/share/kodi
endef

define Package/kodi/install
	$(INSTALL_DIR) $(1)/etc/init.d $(1)/usr/lib/kodi $(1)/usr/share/kodi
	$(INSTALL_BIN) ./files/kodi.init $(1)/etc/init.d/kodi
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/kodi/* $(1)/usr/lib/kodi
	$(CP) $(PKG_INSTALL_DIR)/usr/share/kodi/* $(1)/usr/share/kodi
	mkdir -p $(1)/.kodi/{addons,userdata}
endef

define Package/kodi/conffiles
/.kodi/addons
/.kodi/userdata
endef

$(eval $(call BuildPackage,kodi))
