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
PKG_RELEASE:=20221028
PKG_LIBC:=musl

PKG_SOURCE:=shadowsocks-v$(PKG_VERSION).$(ARCH)-unknown-linux-$(PKG_LIBC).tar.xz
PKG_SOURCE_URL:=https://github.com/shadowsocks/shadowsocks-rust/releases/download/v$(PKG_VERSION)/
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)/$(BUILD_VARIANT)/$(PKG_NAME)-$(PKG_VERSION)-$(PKG_RELEASE)
PKG_HASH:=skip

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
	SECTION:=net
	CATEGORY:=Network
	TITLE:=Lightweight Secured Socks5 Proxy - Rust.
	URL:=https://github.com/shadowsocks/shadowsocks-rust
	DEPENDS:=+libpthread +libc +libgcc +libstdccp +libm
endef

<<<<<<< HEAD
define Build/Compile
	$(call Build/Compile/Default,TARGET="release") 
endef

=======
>>>>>>> buildFix(Makefile): fig step install ss-rust package
define Package/$(PKG_NAME)/config
	config SS_RUST_TOOLS
		depends on PACKAGE_shadowsocks-rust
		bool "Build ssurl"
endef

define Package/$(PKG_NAME)/description
This is a port of shadowsocks.
endef

define Build/Prepare
	tar -C $(PKG_BUILD_DIR)/ -Jxf $(DL_DIR)/$(PKG_SOURCE)
endef

define Build/Compile
	echo "$(PKG_NAME) Compile Skiped!"
endef

define Package/$(PKG_NAME)/conffiles
/etc/config/shadowsocks
endef

define Package/$(PKG_NAME)/postinst
#!/bin/sh
if [ -z "$${IPKG_INSTROOT}" ]; then
	if [ -f /etc/uci-defaults/$(PKG_NAME) ]; then
		( . /etc/uci-defaults/$(PKG_NAME) ) && \
		rm -f /etc/uci-defaults/$(PKG_NAME)
	fi
fi
exit 0
endef

define Package/$(PKG_NAME)/install

<<<<<<< HEAD
	$(call Build/Install/Default,install TARGET="release" PREFIX="/usr/bin")
	
=======
>>>>>>> buildFix(Makefile): fig step install ss-rust package
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) ./files/shadowsocks.track $(1)/usr/bin/ss-local-track

<<<<<<< HEAD
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/shadowsocks.init $(1)/etc/init.d/shadowsocks
	
	$(INSTALL_DIR) $(1)/etc/config
	touch  $(1)/etc/config/shadowsocks
=======
	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/uci-defaults $(1)/etc/uci-defaults/$(PKG_NAME)

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/shadowsocks.init $(1)/etc/init.d/shadowsocks

	$(INSTALL_DIR) $(1)/etc/config
	touch  $(1)/etc/config/shadowsocks

ifeq ($(CONFIG_SS_RUST_TOOLS),y)
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/ssurl $(1)/usr/bin/
endif
>>>>>>> buildFix(Makefile): fig step install ss-rust package
endef

$(eval $(call BuildPackage,$(PKG_NAME)))