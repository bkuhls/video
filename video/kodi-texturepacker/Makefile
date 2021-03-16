#
# Copyright (C) 2017  Stijn Tintel <stijn@linux-ipv6.be>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=kodi-texturepacker
PKG_CODENAME:=Matrix
PKG_VERSION:=19.0
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://github.com/xbmc/xbmc/archive/$(PKG_VERSION)-$(PKG_CODENAME)
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_CODENAME).tar.gz
PKG_HASH:=f7ef8a6f45862ae3b7ebfce4950d74f534be3cb4a0e67ce640963746b3f668f2

HOST_BUILD_DIR:=$(BUILD_DIR_HOST)/$(PKG_NAME)-$(PKG_VERSION)-$(PKG_CODENAME)

PKG_LICENSE:=GPL-2
PKG_LICENSE_FILES:=LICENSE.GPL

PKG_BUILD_PARALLEL:=1
PKG_CHECK_FORMAT_SECURITY:=0
CMAKE_BINARY_SUBDIR:=openwrt-build

HOST_BUILD_DEPENDS:=giflib/host libjpeg-turbo/host lzo/host libpng/host zlib

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/cmake.mk

TAR_OPTIONS:=--strip-components 1 $(TAR_OPTIONS)
TAR_CMD=$(HOST_TAR) -C $(1) $(TAR_OPTIONS)

define Package/kodi-texturepacker
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=kodi-texturepacker
  MENU:=0
endef

CMAKE_HOST_OPTIONS:= \
	-DCMAKE_MODULE_PATH=$(HOST_BUILD_DIR)/cmake/modules \
	-DCORE_SOURCE_DIR=$(HOST_BUILD_DIR) \
	-DCMAKE_CXX_STANDARD=11

HOST_CMAKE_SOURCE_DIR:=$(HOST_BUILD_DIR)/tools/depends/native/TexturePacker
HOST_CFLAGS+=-DTARGET_POSIX -I$(HOST_BUILD_DIR)/xbmc/linux
HOST_LDFLAGS+=-Wl$(comma)-rpath=$(STAGING_DIR_HOSTPKG)/lib

EXTRA_CPPFLAGS += -D_GNU_SOURCE -D__NEED_FILE -DMESA_EGL_NO_X11_HEADERS

define Host/Install
	$(INSTALL_DIR) $(STAGING_DIR_HOSTPKG)/bin
	$(INSTALL_BIN) $(HOST_BUILD_DIR)/TexturePacker $(STAGING_DIR_HOSTPKG)/bin
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,$(PKG_NAME)))
