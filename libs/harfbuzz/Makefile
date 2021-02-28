# Copyright (C) 2021 Bernd Kuhls <bernd.kuhls@t-online.de>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=harfbuzz
PKG_VERSION:=2.7.4
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://github.com/$(PKG_NAME)/$(PKG_NAME)/releases/download/$(PKG_VERSION)
PKG_HASH:=6ad11d653347bd25d8317589df4e431a2de372c0cf9be3543368e07ec23bb8e7

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_MAINTAINER:=Bernd Kuhls <bernd.kuhls@t-online.de>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=COPYING

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1
PKG_BUILD_DEPENDS:=meson/host

include $(INCLUDE_DIR)/package.mk
include ../../../../feeds/packages/devel/meson/meson.mk

define Package/harfbuzz
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Text shaping engine
  URL:=https://harfbuzz.github.io/
  DEPENDS:=+fontconfig +libfreetype
endef

define Package/harfbuzz/description
HarfBuzz is an OpenType text shaping engine
endef

MESON_ARGS += \
  -Dbenchmark=disabled \
  -Dcairo=disabled \
  -Dcoretext=disabled \
  -Ddirectwrite=disabled \
  -Ddocs=disabled \
  -Dexperimental_api=false \
  -Dfontconfig=enabled \
  -Dfreetype=enabled \
  -Dfuzzer_ldflags="" \
  -Dgdi=disabled \
  -Dglib=disabled \
  -Dgobject=disabled \
  -Dgraphite=disabled \
  -Dicu=disabled \
  -Dicu_builtin=false \
  -Dintrospection=disabled \
  -Dtests=disabled

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/$(PKG_NAME)
	$(CP) $(PKG_INSTALL_DIR)/usr/include/$(PKG_NAME)/*.h $(1)/usr/include/$(PKG_NAME)/

	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libharfbuzz*.so* $(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/lib/cmake/$(PKG_NAME)
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/cmake/$(PKG_NAME)/* $(1)/usr/lib/cmake/$(PKG_NAME)/

	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/harfbuzz*.pc $(1)/usr/lib/pkgconfig/
endef

define Package/harfbuzz/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libharfbuzz*.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,harfbuzz))
