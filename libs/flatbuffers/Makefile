# Copyright (C) 2021 Bernd Kuhls <bernd.kuhls@t-online.de>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=flatbuffers
PKG_VERSION:=1.12.0
PKG_RELEASE:=1

PKG_MAINTAINER:=Bernd Kuhls <bernd.kuhls@t-online.de>
PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=LICENSE.txt

PKG_SOURCE_URL:=https://github.com/google/flatbuffers/archive/v$(PKG_VERSION)/
PKG_SOURCE:=flatbuffers-$(PKG_VERSION).tar.gz
PKG_HASH:=62f2223fb9181d1d6338451375628975775f7522185266cd5296571ac152bc45

HOST_BUILD_DIR:=$(BUILD_DIR_HOST)/flatbuffers-$(PKG_VERSION)
PKG_BUILD_DIR:=$(BUILD_DIR)/flatbuffers-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/flatbuffers
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=flatbuffers
  DEPENDS:=+libstdcpp
  URL:=http://google.github.io/flatbuffers/
endef

define Package/flatbuffers/description
FlatBuffers is an efficient cross platform serialization
library for C++, C#, C, Go, Java, JavaScript, PHP, and
Python. It was originally created at Google for game
development and other performance-critical applications.
endef

CMAKE_HOST_OPTIONS:= \
	-DCMAKE_CXX_FLAGS="-std=c++11" \
	-DFLATBUFFERS_BUILD_FLATLIB=OFF \
	-DFLATBUFFERS_BUILD_FLATC=ON \
	-DFLATBUFFERS_BUILD_FLATHASH=OFF \
	-DFLATBUFFERS_BUILD_GRPCTEST=OFF \
	-DFLATBUFFERS_BUILD_SHAREDLIB=OFF \
	-DFLATBUFFERS_BUILD_TESTS=OFF

CMAKE_OPTIONS:= \
	-DCMAKE_CXX_FLAGS="-std=c++11" \
	-DFLATBUFFERS_BUILD_SHAREDLIB=ON \
	-DFLATBUFFERS_BUILD_TESTS=OFF

define Host/Install
	$(INSTALL_DIR) $(STAGING_DIR_HOSTPKG)/bin/
	$(INSTALL_BIN) $(HOST_BUILD_DIR)/flatc $(STAGING_DIR_HOSTPKG)/bin/
endef

define Build/InstallDev
	$(INSTALL_DIR) \
	  $(1)/usr/bin \
	  $(1)/usr/include/$(PKG_NAME) \
	  $(1)/usr/lib/cmake/$(PKG_NAME)

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/bin/* \
	  $(1)/usr/bin/

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/include/$(PKG_NAME)/* \
	  $(1)/usr/include/$(PKG_NAME)/

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/*.so* \
	  $(1)/usr/lib/

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/cmake/$(PKG_NAME)/* \
	  $(1)/usr/lib/cmake/$(PKG_NAME)
endef

define Package/flatbuffers/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so* $(1)/usr/lib/
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,$(PKG_NAME)))
