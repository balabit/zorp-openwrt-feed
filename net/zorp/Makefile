#
# Copyright (C) 2014-2015 BalaBit IT Security
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=zorp
PKG_VERSION:=6.0.0
PKG_BUILD_DIR := $(BUILD_DIR)/$(PKG_NAME)

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/balabit/zorp.git
PKG_SOURCE_SUBDIR:=zorp
PKG_SOURCE_VERSION:=90b8955049cef89ac29a43dbfba0aea43625a537
PKG_SOURCE_PROTO:=git

PKG_LICENSE:=GPLv2

PKG_INSTALL:=1

TARGET_CFLAGS += -I$(STAGING_DIR)/usr/include/zorp -std=c++11 -fPIC
TARGET_LDFLAGS += -L$(STAGING_DIR)/usr/lib -pthread -lz

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/zorp
	CATEGORY:=Network
	SUBMENU:=Firewall
	TITLE:=zorp
	BUILD_DEPENDS:= +gperf
	DEPENDS:= +libstdcpp +glib2 +libopenssl +libpthread +python +libzorpll +python-radix +pydns +pyopenssl +kzorp
endef

define Build/Configure
	(cd $(PKG_BUILD_DIR); ./autogen.sh)
	$(call Build/Configure/Default,--with-pidfiledir=/var/run)
endef

define Package/zorp/install
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_DIR) $(1)/usr
	$(INSTALL_DIR) $(1)/etc/iproute2
	touch $(1)/etc/iproute2/group
	$(CP) $(PKG_INSTALL_DIR)/usr/* $(1)/usr/
	$(CP) $(PKG_INSTALL_DIR)/etc/* $(1)/etc/
endef

$(eval $(call BuildPackage,zorp))
