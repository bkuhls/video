# Copyright (C) 2019 Lucian Cristian <lucian.cristian@gmail.com>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=mesa
PKG_VERSION:=21.0.3
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://mesa.freedesktop.org/archive/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_HASH:=565c6f4bd2d5747b919454fc1d439963024fc78ca56fd05158c3b2cde2f6912b

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1
PKG_BUILD_DEPENDS:=python3/host
HOST_PYTHON3_PACKAGE_BUILD_DEPENDS:=./Mako.txt

PKG_CONFIG_DEPENDS:= \
	CONFIG_PACKAGE_mesa_freedreno \
	CONFIG_PACKAGE_mesa_intel_i915 \
	CONFIG_PACKAGE_mesa_intel_i965 \
	CONFIG_PACKAGE_mesa_intel_vulkan \
	CONFIG_PACKAGE_mesa_radeon_r300 \
	CONFIG_PACKAGE_mesa_radeon_r600 \
	CONFIG_PACKAGE_mesa_nouveau \
	CONFIG_PACKAGE_mesa_swrast \
	CONFIG_PACKAGE_mesa_vc4

include $(INCLUDE_DIR)/package.mk
include ../../../../feeds/packages/lang/python/python3-package.mk
include ../../../../feeds/packages/devel/meson/meson.mk

define Package/mesa/Default
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=mesa
  TITLE:=Mesa DRI OpenGL library
  URL:=https://www.mesa3d.org
endef

define Package/mesa
  $(call Package/mesa/Default)
  MENU:=1
  DEPENDS:=+libdrm +libstdcpp +zlib +libexpat +libatomic \
    $(if $(CONFIG_PACKAGE_libzstd),+libzstd)
endef

define Package/mesa/description
    Mesa is an open-source implementation of the OpenGL specification.
endef

define Package/mesa-freedreno
  $(call Package/mesa/Default)
  DEPENDS+=@(arm||armeb||aarch64)
  TITLE:=MESA freedreno support
endef

ifdef CONFIG_PACKAGE_mesa-freedreno
  _gallium_drivers+=freedreno
  drv_opts+=-Dgallium-xa=enabled
endif

define Package/mesa-intel-i915
  $(call Package/mesa/Default)
  DEPENDS+=@TARGET_x86 +@LIBDRM_INTEL
  TITLE:=MESA Intel i915 support
endef

ifdef CONFIG_PACKAGE_mesa-intel-i915
  _dri_drivers+=i915
endif

define Package/mesa-intel-i965
  $(call Package/mesa/Default)
  DEPENDS+=@TARGET_x86
  TITLE:=MESA Intel i965 support
endef

ifdef CONFIG_PACKAGE_mesa-intel-i965
  _dri_drivers+=i965
endif

define Package/mesa-intel-vulkan
  $(call Package/mesa/Default)
  DEPENDS+=@TARGET_x86
  TITLE:=MESA Intel vulkan support
endef

ifdef CONFIG_PACKAGE_mesa-intel-vulkan
  _vulkan_drivers+=intel
endif

define Package/mesa-radeon-r300
  $(call Package/mesa/Default)
  DEPENDS+=@TARGET_x86 +kmod-drm-radeon +@LIBDRM_RADEON
  TITLE:=MESA Radeon r300 support
endef

ifdef CONFIG_PACKAGE_mesa-radeon-r300
  _gallium_drivers+=r300
endif

define Package/mesa-radeon-r600
  $(call Package/mesa/Default)
  DEPENDS+=@TARGET_x86 +kmod-drm-radeon +@LIBDRM_RADEON
  TITLE:=MESA Radeon r600 support
endef

ifdef CONFIG_PACKAGE_mesa-radeon-r600
  _gallium_drivers+=r600
endif

define Package/mesa-nouveau
  $(call Package/mesa/Default)
  DEPENDS+=@TARGET_x86  +kmod-drm-nouveau +@LIBDRM_NOUVEAU
  TITLE:=MESA nouveau support
endef

ifdef CONFIG_PACKAGE_mesa-nouveau
  _gallium_drivers+=nouveau
 _drv_opts+=-Dgallium-xa=enabled
endif

define Package/mesa-swrast
  $(call Package/mesa/Default)
  DEPENDS+=
  TITLE:=MESA swrast support
endef

ifdef CONFIG_PACKAGE_mesa-swrast
  _gallium_drivers+=swrast
endif

define Package/mesa-vc4
  $(call Package/mesa/Default)
  DEPENDS+=@(arm||armeb||aarch64)
  TITLE:=MESA vc4 support
endef

ifdef CONFIG_PACKAGE_mesa-vc4
  _gallium_drivers+=vc4
endif

MESON_ARGS += \
  -Dshared-glapi=enabled \
  -Dgbm=enabled \
  -Dglx=disabled \
  -Dgles1=enabled \
  -Dgles2=enabled \
  -Degl=enabled \
  -Ddri3=disabled \
  -Dgallium-xvmc=disabled \
  $(_drv_opts) \
  -Dplatforms="" \
  -Dllvm=disabled \
  $(if $(CONFIG_PACKAGE_libzstd),-Dzstd=enabled,-Dzstd=disabled) \
  -Ddri-drivers="$(subst $(space),$(comma),$(_dri_drivers))" \
  -Dgallium-drivers="$(subst $(space),$(comma),$(_gallium_drivers))" \
  -Dvulkan-drivers="$(subst $(space),$(comma),$(_vulkan_drivers))"

define Build/Configure
	$(call HostPython3/PipInstall,$(PYTHON3_PKG_HOST_PIP_INSTALL_ARGS))
	$(call Build/Configure/Meson)
endef

define Build/InstallDev
	$(INSTALL_DIR) \
	  $(1)/usr/include \
	  $(1)/usr/lib

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/include/* \
	  $(1)/usr/include/

	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/{pkgconfig,*.so*} \
	  $(1)/usr/lib/
endef

define Package/mesa/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib \
	  $(1)/usr/share/drirc.d
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/libg*.so* \
	  $(1)/usr/lib/
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/lib{E,G}*.so* \
	  $(1)/usr/lib/
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/share/drirc.d \
	  $(1)/usr/share/
endef

define Package/mesa-freedreno/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib/dri
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/dri/{msm_dri.so,kgsl_dri.so} \
	  $(1)/usr/lib/dri/
endef

define Package/mesa-intel-i915/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib/dri
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/dri/i915_dri.so \
	  $(1)/usr/lib/dri/
endef

define Package/mesa-intel-i965/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib/dri
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/dri/i965_dri.so \
	  $(1)/usr/lib/dri/
endef

define Package/mesa-intel-vulkan/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib \
	  $(1)/usr/share/vulkan/icd.d
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/libvulkan_intel.so \
	  $(1)/usr/lib/
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/share/vulkan/icd.d/intel*.json \
	  $(1)/usr/share/vulkan/icd.d/
endef

define Package/mesa-radeon-r300/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib/dri
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/dri/r300_dri.so \
	  $(1)/usr/lib/dri/
endef

define Package/mesa-radeon-r600/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib/dri
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/dri/r600*.so \
	  $(1)/usr/lib/dri/
endef

define Package/mesa-nouveau/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib/dri
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/dri/nouveau*.so \
	  $(1)/usr/lib/dri/
endef

define Package/mesa-swrast/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib/dri
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/dri/*swrast*.so \
	  $(1)/usr/lib/dri/
endef

define Package/mesa-vc4/install
	$(INSTALL_DIR) \
	  $(1)/usr/lib/dri
	$(CP) \
	  $(PKG_INSTALL_DIR)/usr/lib/dri/vc4_dri.so \
	  $(1)/usr/lib/dri/
endef

$(eval $(call BuildPackage,mesa))
$(eval $(call BuildPackage,mesa-freedreno))
$(eval $(call BuildPackage,mesa-intel-i915))
$(eval $(call BuildPackage,mesa-intel-i965))
$(eval $(call BuildPackage,mesa-intel-vulkan))
$(eval $(call BuildPackage,mesa-radeon-r300))
$(eval $(call BuildPackage,mesa-radeon-r600))
$(eval $(call BuildPackage,mesa-nouveau))
$(eval $(call BuildPackage,mesa-swrast))
$(eval $(call BuildPackage,mesa-vc4))
