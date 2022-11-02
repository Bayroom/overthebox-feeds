include $(TOPDIR)/rules.mk

PKG_NAME:=mptcpd
PKG_VERSION:=0.11
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/intel/mptcpd/releases/download/v$(PKG_VERSION)
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_HASH:=043b6f265b02135f942016b4aaa4703c7e9add0cf790331b7d97d334f92a038a
PKG_FIXUP:=autoreconf
PKG_FORTIFY_SOURCE:=0

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
	SECTION:=net
	CATEGORY:=Network
	TITLE:=Multipath TCP Deamon
	DEPENDS:=+argp-standalone +ell 
	URL:=https://github.com/intel/mptcpd
endef

define Package/$(PKG_NAME)/description
	The Multipath TCP Daemon - mptcpd - is a daemon for Linux based operating systems
	that performs multipath TCP path management related operations in the user space.
	It interacts with the Linux kernel through a generic netlink connection
	to track per-connection information (e.g. available remote addresses),
	available network interfaces, request new MPTCP subflows, handle requests for subflows, etc.
endef

define Build/Configure
	$(call Build/Configure/Default, --with-kernel=upstream --disable-stack-protection)
endef


define Package/$(PKG_NAME)/install

	mkdir -p $(1)/etc/mptcpd
	$(INSTALL_DIR) $(1)/etc/mptcpd/
	$(CP) $(PKG_BUILD_DIR)/etc/mptcpd.conf $(1)/etc/mptcpd/

	$(INSTALL_DIR) $(1)/bin
	$(CP) $(PKG_BUILD_DIR)/src/mptcpize $(1)/bin/

	mkdir -p $(1)/usr/libexec
	$(INSTALL_DIR) $(1)/usr/libexec/
	$(CP) $(PKG_BUILD_DIR)/src/mptcpd $(1)/usr/libexec/

endef

$(eval $(call BuildPackage,$(PKG_NAME)))
