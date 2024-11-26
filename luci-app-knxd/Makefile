include $(TOPDIR)/rules.mk

PKG_NAME:=luci-app-knxd
PKG_VERSION:=0.2.6
PKG_RELEASE:=2
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/luci-app-knxd
  SECTION:=luci
  CATEGORY:=LuCI
  SUBMENU:=3. Applications
  TITLE:=Eib KNX deamon
  URL:=https://github.com/knxd/knxd/wiki
  EXTRA_DEPENDS:=knxd, luci-mod-admin-full, luci-lib-nixio, luci-compat
  PKGARCH:=all
endef

define Build/Prepare
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/luci-app-knxd/postinst
#!/bin/sh
[ -n "${IPKG_INSTROOT}" ] || {
	rm -f /tmp/luci-indexcache
	exit 0
}

endef

define Package/luci-app-knxd/install
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/controller
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/model/cbi
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/view
	$(INSTALL_BIN) ./luasrc/controller/knxd.lua $(1)/usr/lib/lua/luci/controller
	$(INSTALL_BIN) ./luasrc/model/cbi/knxd.lua $(1)/usr/lib/lua/luci/model/cbi
	$(INSTALL_BIN) ./luasrc/view/knxd_diag.htm $(1)/usr/lib/lua/luci/view
	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) files/etc/uci-defaults/luci-app-knxd $(1)/etc/uci-defaults/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) files/etc/init.d/knxd-ini $(1)/etc/init.d/
endef

$(eval $(call BuildPackage,luci-app-knxd))
