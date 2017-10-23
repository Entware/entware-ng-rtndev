#
# Copyright (C) 2017 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=httpry
PKG_VERSION:=0.1.8
PKG_REV:=2ba7afab870880565e7efa0d9b55ba820d38bb1d
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_URL:=https://github.com/jbittel/httpry.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_VERSION:=$(PKG_REV)

include $(INCLUDE_DIR)/package.mk

define Package/httpry
	SECTION:=net
	CATEGORY:=Network
	DEPENDS:=+libpcap +libpthread
	TITLE:=HTTP logging and information retrieval tool
	URL:=http://dumpsterventures.com/jason/httpry/
	MAINTAINER:=Entware team, http://entware.net
endef

define Package/httpry/description
 httpry is a specialized packet sniffer designed for displaying and logging
 HTTP traffic. It is not intended to perform analysis itself, but to capture,
 parse, and log the traffic for later analysis.
endef


define Package/httpry/install
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/$(PKG_NAME) $(1)/opt/sbin
endef

$(eval $(call BuildPackage,httpry))
