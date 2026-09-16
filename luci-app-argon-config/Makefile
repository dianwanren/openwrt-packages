include $(TOPDIR)/rules.mk

PKG_NAME:=luci-app-argon-config
PKG_VERSION:=1.0
PKG_RELEASE:=20230608

PKG_MAINTAINER:=jerrykuku <jerrykuku@qq.com>

LUCI_TITLE:=LuCI app for Argon theme configuration
LUCI_PKGARCH:=all
LUCI_DEPENDS:=+luci-theme-argon

define Package/$(PKG_NAME)/conffiles
/etc/config/argon
endef

# 有些构建环境（Windows 下复制文件、SMB/CIFS 挂载、zip 解压等）会丢掉源码里的
# 可执行位。rpcd 是用 execv 直接执行 /usr/libexec/rpcd/<name> 的，权限不对时整个
# luci.argon 对象都不可用：页面「可用空间」恒为 0 B，上传/删除背景也会失败。
# 这里在编译期强制补回 0755，不受源码树权限影响。
define Build/Prepare/$(LUCI_NAME)
	chmod 0755 $(PKG_BUILD_DIR)/root/usr/libexec/rpcd/luci.argon 2>/dev/null || true
endef

define Build/Compile
	@mkdir -p $(PKG_BUILD_DIR)/po/ru
	@if [ -f "Package/$(PKG_NAME)/po/ru/argon-config.po" ]; then \
		$(STAGING_DIR_HOSTPKG)/bin/po2lmo \
			"Package/$(PKG_NAME)/po/ru/argon-config.po" \
			"$(PKG_BUILD_DIR)/po/ru/argon-config.lmo"; \
	fi
endef

include $(TOPDIR)/feeds/luci/luci.mk

# call BuildPackage - OpenWrt buildroot signature
