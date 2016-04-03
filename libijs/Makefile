#
# Copyright (C) 2011-2016 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ijs
PKG_VERSION:=0.35
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.openprinting.org/download/ijs/download/
PKG_MD5SUM:=0cc4dfdb3d5aadf39c9334fa95098c20
PKG_LICENSE:=free of charge Copyright (c) 2001-2002 artofcode LLC

PKG_INSTALL:=1

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk

define Package/libijs
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=IJS is a protocol for transmission of raster page images.
  DEPENDS:=+gcc 
  URL:=	http://www.openprinting.org
  SUBMENU:=Printing
endef

define Package/libijs/description
IJS is, first and foremost, a protocol for transmission of raster page images.
endef

CONFIGURE_ARGS += \

define Build/Compile
	$(call Build/Compile/Default,)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(PKG_INSTALL_DIR)/opt/bin/ijs-config $(1)/opt/bin/
	$(SED) \
		's,^\(prefix\|exec_prefix\)=.*,\1=$(STAGING_DIR)/opt,g' \
		$(1)/opt/bin/ijs-config

	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/ijs $(1)/opt/include/

	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libijs.{a,la} $(1)/opt/lib/

	$(INSTALL_DIR) $(1)/opt/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/pkgconfig/ijs.pc $(1)/opt/lib/pkgconfig/

	$(INSTALL_DIR) $(2)/bin
	for f in ijs-config; do \
		$(LN) ../../opt/bin/$$$$f $(2)/bin/ ; \
	done
endef


define Package/libijs/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/* $(1)/opt/lib/
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,libijs))
