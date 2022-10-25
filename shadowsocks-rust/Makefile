#
# Copyright (C) 2022 OVHvloud 
#
# This is free software, licensed under the GNU General Public License v3.
# See /LICENSE for more information.
# This software was inspired from <honwen> <https://github.com/honwen>
#

include $(TOPDIR)/rules.mk

PKG_NAME:=shadowsocks-rust
PKG_VERSION:=1.14.3
PKG_RELEASE:=20221025
PKG_LIBC:=musl

PKG_SOURCE:=v$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/shadowsocks/shadowsocks-rust/archive/refs/tags/
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)/$(BUILD_VARIANT)/$(PKG_NAME)-$(PKG_VERSION)
PKG_HASH:=a41437cdae1279914f11c07a584ab8b2b21e9b08bd732ef11fb447c765202215

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
	SECTION:=net
	CATEGORY:=Network
	TITLE:=Lightweight Secured Socks5 Proxy - Rust.
	URL:=https://github.com/shadowsocks/shadowsocks-rust
endef

define Build/Compile
	$(call Build/Compile/Default,TARGET=release)
endef

define Build/install
<<<<<<< HEAD
	$(call Build/Install/Default,install install-TARGET=release)
=======
	$(call Build/Install/Default,install TARGET=release)
>>>>>>> fix(Makefile): specify target for cargo build
endef

define Package/$(PKG_NAME)/config
	config SS_RUST_TOOLS
		depends on PACKAGE_shadowsocks-rust
		bool "Build ssurl"
endef

define Package/$(PKG_NAME)/description
This is a port of shadowsocks.
endef

define Package/$(PKG_NAME)/conffiles
/etc/config/shadowsocks
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ssservice $(1)/usr/bin/
	$(INSTALL_BIN) ./files/shadowsocks.track $(1)/usr/bin/ss-local-track
	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/uci-defaults $(1)/etc/uci-defaults/$(PKG_NAME)
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/shadowsocks.init $(1)/etc/init.d/shadowsocks
	$(INSTALL_DIR) $(1)/etc/config
	touch  $(1)/etc/config/shadowsocks
ifeq ($(CONFIG_SS_RUST_TOOLS),y)
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ssurl $(1)/usr/bin/
endif
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
