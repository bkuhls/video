# Copyright (C) 2021 Bernd Kuhls <bernd.kuhls@t-online.de>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=fstrcmp
PKG_VERSION_MAJOR:=0.7
PKG_VERSION:=$(PKG_VERSION_MAJOR).D001
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://sourceforge.net/projects/$(PKG_NAME)/files/$(PKG_NAME)/$(PKG_VERSION_MAJOR)
PKG_HASH:=e4018e850f80700acee8da296e56e15b1eef711ab15157e542e7d7e1237c3476

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_MAINTAINER:=Bernd Kuhls <bernd.kuhls@t-online.de>
PKG_LICENSE:=GPL-3.0+
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/fstrcmp
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=A library that is used to make fuzzy comparisons of strings and byte arrays
  URL:=http://fstrcmp.sourceforge.net/
endef

define Package/fstrcmp/description
The fstrcmp project provides a library that is used to make
fuzzy comparisons of strings and byte arrays, including multi-
byte character strings.
endef

define Build/Compile
	$(call Build/Compile/Default, \
		all-bin libdir/pkgconfig/fstrcmp.pc
	+$(MAKE) -i $(PKG_JOBS) -C $(PKG_BUILD_DIR) \
		DESTDIR="$(PKG_INSTALL_DIR)" \
		install)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/*.h $(1)/usr/include/

	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libfstrcmp.{a,so*} $(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/fstrcmp.pc $(1)/usr/lib/pkgconfig/
endef

define Package/fstrcmp/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libfstrcmp.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,fstrcmp))
