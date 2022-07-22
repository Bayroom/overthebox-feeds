include $(TOPDIR)/rules.mk

PKG_NAME:=overthebox
PKG_VERSION:=0.70
PKG_RELEASE:=0

include $(INCLUDE_DIR)/package.mk

MY_DEPENDS := \
    graph glorytun  mptcp shadowsocks-libev  \
    kmod-macvlan jq curl ca-bundle ca-certificates \
    @LIBCURL_THREADED_RESOLVER

define Package/$(PKG_NAME)
SECTION:=OVH
CATEGORY:=OverTheBox
DEPENDS:=$(foreach p,$(MY_DEPENDS),+$(p))
TITLE:=OverTheBox
endef

define Package/$(PKG_NAME)/description
OverTheBox package
endef

define Package/$(PKG_NAME)/conffiles
/etc/config/$(PKG_NAME)
endef

define Build/Compile
endef

define Package/$(PKG_NAME)/install
	#copy the content of "files/" except etc/udhcpc.user
	$(CP) ./files/bin/* $(1)/
	$(CP) ./files/etc/hotplug.d/* $(1)/
	$(CP) ./files/etc/init.d/* $(1)/
	$(CP) ./files/etc/sysctl.d/* $(1)/
	$(CP) ./files/etc/uci-defaults/* $(1)/
	$(CP) ./files/lib/* $(1)/
	$(CP) ./files/usr/* $(1)/
	#copy content of files/etc/udhcpc.user to udhcpc file
	cat ./files/etc/udhcpc.user >> $(1)/../../../root-x86/etc/udhcpc.user
	$(INSTALL_DIR) $(1)/etc/config
	touch $(1)/etc/config/$(PKG_NAME)
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
