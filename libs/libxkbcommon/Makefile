# Copyright (C) 2021 Bernd Kuhls <bernd.kuhls@t-online.de>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=libxkbcommon
PKG_VERSION:=1.0.3
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=http://xkbcommon.org/download
PKG_HASH:=a2202f851e072b84e64a395212cbd976ee18a8ee602008b0bad02a13247dbc52

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1
PKG_BUILD_DEPENDS:=meson/host

include $(INCLUDE_DIR)/package.mk
include ../../../../feeds/packages/devel/meson/meson.mk

define Package/libxkbcommon
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=keymap compiler
  URL:=http://xkbcommon.org/
  MAINTAINER:=Bernd Kuhls <bernd.kuhls@t-online.de>
endef

define Package/libxkbcommon/description
xkbcommon is a keymap compiler and support library which
processes a reduced subset of keymaps as defined by the XKB
specification.
endef

MESON_ARGS += \
	-Denable-docs=false \
	-Denable-wayland=false \
	-Denable-x11=false \
	-Denable-xkbregistry=false

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/
	$(CP) $(PKG_INSTALL_DIR)/usr/include/xkbcommon $(1)/usr/include/

	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib/
endef

define Package/libxkbcommon/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
