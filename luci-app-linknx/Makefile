include $(TOPDIR)/rules.mk

PKG_NAME:=luci-app-linknx
PKG_VERSION:=0.3.2
PKG_RELEASE:=1
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/luci-app-linknx
  SECTION:=luci
  CATEGORY:=LuCI
  SUBMENU:=3. Applications
  TITLE:=linknx daemon
  URL:=https://github.com/linknx/linknx/wiki
  EXTRA_DEPENDS:=linknx-uci, luci-mod-admin-full, collectd-mod-exec, luci-app-statistics, luci-compat
  PKGARCH:=all
endef

define Build/Prepare
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/luci-app-linknx/postinst
#!/bin/sh
[ -n "${IPKG_INSTROOT}" ] || {
	rm -f /tmp/luci-indexcache
	exit 0
}

endef

define Package/luci-app-linknx/install
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/controller
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/model/cbi
	$(INSTALL_DIR) $(1)/usr/lib/lua/luci/view
	$(INSTALL_BIN) ./luasrc/controller/linknx.lua $(1)/usr/lib/lua/luci/controller
	$(INSTALL_BIN) ./luasrc/model/cbi/linknx.lua $(1)/usr/lib/lua/luci/model/cbi
	$(INSTALL_BIN) ./luasrc/model/cbi/linknx_xml.lua $(1)/usr/lib/lua/luci/model/cbi
	$(INSTALL_DATA) ./luasrc/view/linknx_diag.htm $(1)/usr/lib/lua/luci/view
	$(INSTALL_DIR) $(1)/etc/uci-defaults
	$(INSTALL_BIN) ./files/etc/uci-defaults/linknx-uci $(1)/etc/uci-defaults
	$(INSTALL_DIR) $(1)/etc/collectd/conf.d
	$(INSTALL_DATA) ./files/etc/collectd/conf.d/linknx.conf $(1)/etc/collectd/conf.d
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) ./files/usr/bin/linknx-stat.sh $(1)/usr/bin
	$(INSTALL_DIR) $(1)/usr/share/collectd
	$(INSTALL_DATA) ./files/usr/share/collectd/linknx.db $(1)/usr/share/collectd
endef

$(eval $(call BuildPackage,luci-app-linknx))
