#
# Copyright (c) 2015 Affinegy, Inc. All rights reserved.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=rapidjson
PKG_VERSION:=1.1.0
PKG_RELEASE:=1
PKG_SOURCE_URL:=https://github.com/miloyip/$(PKG_NAME)/archive
PKG_SOURCE:=v$(PKG_VERSION).tar.gz
PKG_HASH:=bf7ced29704a1e696fbccf2a2b4ea068e7774fa37f6d7dd4039d0787f8bed98e

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/$(PKG_NAME)
  SECTION:=lib
  CATEGORY:=Libraries
  URL:=https://github.com/miloyip/rapidjson
  TITLE:=rapidjson JSON parser/generator for C++
  MAINTAINER:=Bernd Kuhls <bernd.kuhls@t-online.de>
endef

define Package/$(PKG_NAME)/description
  A fast JSON parser/generator for C++ with both SAX/DOM style API
endef

CMAKE_OPTIONS:= \
	-DRAPIDJSON_BUILD_DOC=OFF \
	-DRAPIDJSON_BUILD_EXAMPLES=OFF \
	-DRAPIDJSON_BUILD_TESTS=OFF

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/include/$(PKG_NAME) $(1)/usr/include/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib/
endef

define Package/rapidjson/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
