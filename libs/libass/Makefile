# Copyright (C) 2017 Stijn Tintel <stijn@linux-ipv6.be>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=libass
PKG_VERSION:=0.15.0
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://github.com/libass/libass/releases/download/$(PKG_VERSION)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_HASH:=9f09230c9a0aa68ef7aa6a9e2ab709ca957020f842e52c5b2e52b801a7d9e833

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libass
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+fontconfig +fribidi +harfbuzz +libfreetype
  TITLE:=libass
  URL:=https://github.com/libass/libass
  MAINTAINER:=Stijn Tintel <stijn@linux-ipv6.be>
endef

ifneq ($(CONFIG_TARGET_x86),)
ifeq ($(CONFIG_NASM),y)
  CONFIGURE_VARS+= AS=nasm
  MAKE_FLAGS+= AS=nasm
else
  CONFIGURE_VARS+= AS=
  MAKE_FLAGS+= AS=
  CONFIGURE_ARGS += --disable-asm
endif
endif

CONFIGURE_ARGS += \
	--enable-fontconfig

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/ass $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/include/ass/*.h $(1)/usr/include/ass/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/{pkgconfig,*.so*} $(1)/usr/lib/
endef

define Package/libass/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libass))
