# Copyright (C) 2021 Bernd Kuhls <bernd.kuhls@t-online.de>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=intel-vaapi-driver
PKG_VERSION:=2.4.1
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://github.com/intel/intel-vaapi-driver/releases/download/$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_HASH:=0081fce08eb3a83f7d99c3b853c8fdfa0af437b8f5b0fb7c66faeb83bcbe0c19

PKG_MAINTAINER:=Bernd Kuhls <bernd.kuhls@t-online.de>
PKG_LICENSE:=MIT

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libva-intel-driver
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libva +libdrm +@LIBDRM_INTEL
  TITLE:=VA-API user mode driver for Intel GEN Graphics family
  URL:=https://01.org/vaapi
endef

CONFIGURE_ARGS += \
  --prefix=/usr \
  --disable-x11 \
  --disable-wayland \
  --disable-static \
  --enable-shared

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/lib/va

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/va/*.so \
	  $(1)/usr/lib/va/
endef

define Package/libva-intel-driver/install
	$(INSTALL_DIR) $(1)/usr/lib/va

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/va/*.so* \
	  $(1)/usr/lib/va/
endef

$(eval $(call BuildPackage,libva-intel-driver))
