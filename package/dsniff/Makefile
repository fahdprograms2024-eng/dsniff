include $(TOPDIR)/rules.mk

PKG_NAME:=dsniff
PKG_VERSION:=2.3
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/dsniff-$(PKG_VERSION)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/fahdprograms2024-eng/dsniff.git
PKG_SOURCE_VERSION:=master
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-$(PKG_SOURCE_VERSION).tar.gz
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)

PKG_MAINTAINER:=OpenWrt dsniff package
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/dsniff
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Network
  TITLE:=dsniff network auditing tools
  URL:=https://github.com/fahdprograms2024-eng/dsniff
  DEPENDS:=+libpcap +libnet +libnids +libopenssl +libdb47
endef

define Package/dsniff/description
dsniff network auditing and testing tools.
endef

CONFIGURE_ARGS += \
	--without-x \
	--with-db="$(STAGING_DIR)/usr" \
	--with-libpcap="$(STAGING_DIR)/usr" \
	--with-libnet="$(STAGING_DIR)/usr" \
	--with-libnids="$(STAGING_DIR)/usr" \
	--with-openssl="$(STAGING_DIR)/usr"

TARGET_CFLAGS += \
	-I$(STAGING_DIR)/usr/include \
	-I$(STAGING_DIR)/usr/include/libpcap

TARGET_LDFLAGS += \
	-L$(STAGING_DIR)/usr/lib

define Package/dsniff/install
	$(INSTALL_DIR) $(1)/usr/sbin

	$(INSTALL_BIN) $(PKG_BUILD_DIR)/arpspoof $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/dnsspoof $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/dsniff $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/filesnarf $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/macof $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/mailsnarf $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/msgsnarf $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/sshow $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/tcpkill $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/tcpnice $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/urlsnarf $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/sshmitm $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/webmitm $(1)/usr/sbin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/webspy $(1)/usr/sbin/

	$(INSTALL_DIR) $(1)/usr/share/dsniff

	$(INSTALL_DATA) \
		$(PKG_BUILD_DIR)/dsniff.magic \
		$(1)/usr/share/dsniff/

	$(INSTALL_DATA) \
		$(PKG_BUILD_DIR)/dsniff.services \
		$(1)/usr/share/dsniff/

	$(INSTALL_DATA) \
		$(PKG_BUILD_DIR)/dnsspoof.hosts \
		$(1)/usr/share/dsniff/

	$(INSTALL_DIR) $(1)/usr/share/man/man8

	$(INSTALL_DATA) \
		$(PKG_BUILD_DIR)/*.8 \
		$(1)/usr/share/man/man8/ 2>/dev/null || true
endef

$(eval $(call BuildPackage,dsniff))
