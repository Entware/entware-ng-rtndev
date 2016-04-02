#
# Copyright (C) 2011-2016 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=cups-filters
PKG_VERSION:=1.8.2
PKG_RELEASE:=1

PKG_SOURCE:=cups-filters-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=http://www.openprinting.org/download/cups-filters/
PKG_MD5SUM:=a32a83aef1808e4ccabad96a593a9f89
PKG_LICENSE:=(L)GPL(2/2+/3/3+)/BSD-4/Expat/The MIT License
PKG_LICENSE:=COPYING

PKG_INSTALL:=1

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk

define Package/cups-filters
  SECTION:=Utils
  CATEGORY:=Utilities
  TITLE:=OpenPrinting CUPS filters
  DEPENDS:=+libiconv-full +libintl-full +cups +libcupsimage +fontconfig +libtiff +libjpeg +libpng +poppler +qpdf +glib2 +lcms +libijs +ghostscript +busybox
  URL:=http://www.openprinting.org
  SUBMENU:=Printing
endef

define Package/cups-filters/description
	CUPS filters maintained by OpenPrinting.
	The CUPS Filters package contains backends, filters and other software that was once part of the core CUPS distribution 
	but is no longer maintained by Apple Inc.
endef

CONFIGURE_ARGS += \
	--with-gs-path=/opt/bin/gs \
	--with-pdftops-path=/opt/bin/gs \

define Build/Compile
	$(CP) $(STAGING_DIR)/opt/lib/libiconv-full/lib/libiconv.{a,so.*} $(STAGING_DIR)/opt/lib	# ugly workaround for not being able to find these libs
	$(CP) $(STAGING_DIR)/opt/lib/libintl-full/lib/libintl.{a,so.*} $(STAGING_DIR)/opt/lib	# i'm sure there's a better way, i just don't know yet...
	$(call Build/Compile/Default,LIBTOOL="./libtool --tag=CC")
endef

define Package/cups-filters/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_DIR) $(1)/opt/etc
	$(INSTALL_DIR) $(1)/opt/lib
	$(INSTALL_DIR) $(1)/opt/sbin/
	$(INSTALL_DIR) $(1)/opt/include/
	$(INSTALL_DIR) $(1)/opt/share
	$(INSTALL_DIR) $(1)/opt/man
	$(CP) $(PKG_INSTALL_DIR)/opt/etc/* $(1)/opt/etc/
	$(CP) $(PKG_INSTALL_DIR)/opt/include/* $(1)/opt/include/
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/* $(1)/opt/lib/
	$(CP) $(PKG_INSTALL_DIR)/opt/share/* $(1)/opt/share/
	$(CP) $(PKG_INSTALL_DIR)/opt/sbin/* $(1)/opt/sbin/
	$(CP) $(PKG_INSTALL_DIR)/opt/man/* $(1)/opt/man/
	# update symlink before installing binary, i quess this also could use some improvement)
	ln -f -s $(PKG_INSTALL_DIR)/opt/lib/cups/filter/foomatic-rip $(PKG_INSTALL_DIR)/opt/bin/foomatic-rip
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/* $(1)/opt/bin/
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(INSTALL_DIR) $(1)/opt/include/cupsfilters
	$(INSTALL_DIR) $(1)/opt/include/fontembed
	$(CP) $(PKG_INSTALL_DIR)/opt/include/cupsfilters/*.h $(1)/opt/include/cupsfilters
	$(CP) $(PKG_INSTALL_DIR)/opt/include/fontembed/*.h $(1)/opt/include/fontembed
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libcupsfilters.{a,la,so*} $(1)/opt/lib/
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libfontembed.{a,la,so*} $(1)/opt/lib/
	$(INSTALL_DIR) $(1)/opt/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/pkgconfig/{libcupsfilters,libfontembed}.pc $(1)/opt/lib/pkgconfig/
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,cups-filters))
