#
# Copyright (C) 2006 OpenWrt.org
# Copyright (C) 2017 Stijn Tintel <stijn@linux-ipv6.be>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=fribidi
PKG_VERSION:=1.0.10
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://github.com/$(PKG_NAME)/$(PKG_NAME)/releases/download/v$(PKG_VERSION)
PKG_HASH:=7f1c687c7831499bcacae5e8675945a39bacbad16ecaa945e9454a32df653c01

PKG_FIXUP:=libtool
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/fribidi
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=GNU FriBidi is an implementation of the Unicode Bidirectional Algorithm (bidi)
  URL:=http://fribidi.org
  MAINTAINER:=Stijn Tintel <stijn@linux-ipv6.be>
endef

CONFIGURE_ARGS += --without-glib
TARGET_CFLAGS += -D_GNU_SOURCE

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/include/fribidi $(1)/usr/include/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/{pkgconfig,*.so*} $(1)/usr/lib/
endef

define Package/fribidi/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,fribidi))
