include $(TOPDIR)/rules.mk

PKG_NAME:=ell
PKG_VERSION:=0.53
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://kernel.googlesource.com/pub/scm/libs/ell/ell.git/+archive
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_HASH:=skip
PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
	SECTION:=libs
	CATEGORY:=Libraries
	TITLE:=Embedded linux library
	URL:=https://kernel.googlesource.com/pub/scm/libs/ell/ell.git
endef

define Build/Prepare
	tar -C $(PKG_BUILD_DIR)/ -xf $(DL_DIR)/$(PKG_SOURCE)
	(cd $(PKG_BUILD_DIR); ./bootstrap)
endef

define Build/InstallDev
	mkdir -p $(1)/usr/include/ell
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_BUILD_DIR)/ell/*h $(1)/usr/include/ell

	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_BUILD_DIR)/ell/ell.pc $(1)/usr/lib/pkgconfig

	$(INSTALL_DIR) $(1)/usr/lib/ 
	$(CP) $(PKG_BUILD_DIR)/ell/.libs/libell.so.0.0.2 $(1)/usr/lib/
	{ cd $(1)/usr/lib/; ln -s -f libell.so.0.0.2 libell.so.0 || { rm -f libell.so.0 && ln -s libell.so.0.0.2 libell.so.0; }; }
	{ cd $(1)/usr/lib/; ln -s -f libell.so.0.0.2 libell.so || { rm -f libell.so && ln -s libell.so.0.0.2 libell.so; }; }
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(PKG_BUILD_DIR)/ell/.libs/libell.so.0.0.2 $(1)/usr/lib/
	{ cd $(1)/usr/lib/; ln -s -f libell.so.0.0.2 libell.so.0 || { rm -f libell.so.0 && ln -s libell.so.0.0.2 libell.so.0; }; }
	{ cd $(1)/usr/lib/; ln -s -f libell.so.0.0.2 libell.so || { rm -f libell.so && ln -s libell.so.0.0.2 libell.so; }; }
		
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
