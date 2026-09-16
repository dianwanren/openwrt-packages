#
# Copyright (C) 2008-2019 Jerrykuku
#
# This is free software, licensed under the Apache License, Version 2.0 .
#

include $(TOPDIR)/rules.mk

LUCI_TITLE:=Argon Theme
LUCI_DEPENDS:=+USE_APK:wget-any +!USE_APK:wget +jsonfilter
PKG_VERSION:=2.4.7
PKG_RELEASE:=20260824

CONFIG_LUCI_CSSTIDY:=

include $(TOPDIR)/feeds/luci/luci.mk

# 同 luci-app-argon-config：构建环境可能丢掉可执行位，rpcd 无法 execv 该脚本，
# 在线壁纸（bing/unsplash/wallhaven）就会静默失效。编译期强制补回 0755。
#
# 必须写在 include luci.mk 之后：define 的名字在解析这一行时就展开，
# $(LUCI_NAME) 是在 luci.mk 里才定义的。
define Build/Prepare/$(LUCI_NAME)
	chmod 0755 $(PKG_BUILD_DIR)/root/usr/libexec/rpcd/luci.argon_wallpaper 2>/dev/null || true
endef

# call BuildPackage - OpenWrt buildroot signature
