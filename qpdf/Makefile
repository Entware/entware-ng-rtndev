#
# Copyright (C) 2011-2016 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk

PKG_NAME:=qpdf
PKG_VERSION:=5.1.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/$(PKG_NAME)
PKG_MD5SUM:=0bd15ef5eea5f628951ab456c84e78ec
PKG_LICENSE:=Version 2.0 of the Artistic License
PKG_INSTALL:=1

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk

define Package/qpdf
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=QPDF is a command-line program for transformations on PDF files.
  DEPENDS:=+libpcre +zlib +libstdcpp
  URL:=http://qpdf.sourceforge.net/
  SUBMENU:=Printing
endef

define Package/qpdf/description
QPDF is a command-line program that does structural, content-preserving transformations on PDF files. 
It could have been called something like pdf-to-pdf.
It also provides  many useful capabilities to developers of PDF-producing software or for people who just want 
to look at the innards of a PDF file to learn more about how they work.
endef

CONFIGURE_ARGS += \
	--with-random=/dev/urandom

define Build/Compile
	$(call Build/Compile/Default,LIBTOOL="./libtool --tag=CC")
endef

define Package/qpdf/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/* $(1)/opt/bin/
	$(INSTALL_DIR) $(1)/opt/include/qpdf	
	$(CP) $(PKG_INSTALL_DIR)/opt/include/qpdf/* $(1)/opt/include/qpdf/
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/* $(1)/opt/lib/
	$(INSTALL_DIR) $(1)/opt/share/doc/qpdf
	$(CP) $(PKG_INSTALL_DIR)/opt/share/doc/qpdf/* $(1)/opt/share/doc/qpdf/
	$(INSTALL_DIR) $(1)/opt/man/man1
	$(CP) $(PKG_INSTALL_DIR)/opt/man/man1/* $(1)/opt/man/man1/
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/qpdf $(1)/opt/include/
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libqpdf.{a,la,so*} $(1)/opt/lib/
	$(INSTALL_DIR) $(1)/opt/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/pkgconfig/libqpdf.pc $(1)/opt/lib/pkgconfig/
	$(SED) \
		's,/opt/include,$$$${prefix}/include,g; \
		 s,/opt/lib,$$$${exec_prefix}/lib,g' \
		 $(1)/opt/lib/pkgconfig/libqpdf.pc
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,qpdf))
