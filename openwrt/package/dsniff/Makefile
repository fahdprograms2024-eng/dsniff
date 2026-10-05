include $(TOPDIR)/rules.mk

PKG_NAME:=dsniff
PKG_VERSION:=2.3
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/fahdprograms2024-eng/dsniff.git
PKG_SOURCE_VERSION:=master
PKG_SOURCE_SUBMODULES:=0

PKG_MAINTAINER:=Fahd Programs
PKG_LICENSE:=BSD-3-Clause
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk


define Package/dsniff
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Network
  TITLE:=dsniff network auditing tools
  URL:=https://github.com/fahdprograms2024-eng/dsniff
  DEPENDS:=+libpcap +libnet +libnids +libopenssl
endef


define Package/dsniff/description
  dsniff is a collection of network auditing tools.
  This package is built from the fahdprograms2024-eng/dsniff fork.
endef


CONFIGURE_ARGS += \
	--without-x \
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

	$(INSTALL_BIN) $(PKG_BUILD_DIR)/arpspoof \
		$(1)/usr/sbin/

	$(INSTALL_BIN) $(PKG_BUILD_DIR)/dnsspoof \
		$(1)/usr/sbin/

	$(INSTALL_BIN) $(PKG_BUILD_DIR)/dsniff \
		$(1)/usr/sbin/

	$(INSTALL_BIN) $(PKG_BUILD_DIR)/filesnarf \
		$(1)/usr/sbin/

	$(INSTALL_BIN) $(PKG_BUILD_DIR)/macof \
		$(1)/usr/sbin/

	$(INSTALL_BIN) $(PKG_BUILD_DIR)/mailsnarf \
		$(1)/usr/sbin/

	$(INSTALL_BIN) $(PKG_BUILD_DIR)/msgsnarf \
		$(1)/usr/sbin/

	$(INSTALL_BIN) $(PKG_BUILD_DIR)/sshow \
		$(1)/usr/sbin/

	$(INSTALL_BIN) $(PKG_BUILD_DIR)/tcpkill \
		$(1)/usr/sbin/

	$(INSTALL_BIN) $(PKG_BUILD_DIR)/tcpnice \
		$(1)/usr/sbin/

	$(INSTALL_BIN) $(PKG_BUILD_DIR)/urlsnarf \
		$(1)/usr/sbin/

	$(INSTALL_BIN) $(PKG_BUILD_DIR)/sshmitm \
		$(1)/usr/sbin/

	$(INSTALL_BIN) $(PKG_BUILD_DIR)/webmitm \
		$(1)/usr/sbin/

	$(INSTALL_BIN) $(PKG_BUILD_DIR)/webspy \
		$(1)/usr/sbin/


	$(INSTALL_DIR) $(1)/usr/lib/dsniff

	$(INSTALL_DATA) $(PKG_BUILD_DIR)/dsniff.magic \
		$(1)/usr/lib/dsniff/

	$(INSTALL_DATA) $(PKG_BUILD_DIR)/dsniff.services \
		$(1)/usr/lib/dsniff/

	$(INSTALL_DATA) $(PKG_BUILD_DIR)/dnsspoof.hosts \
		$(1)/usr/lib/dsniff/


	$(INSTALL_DIR) $(1)/usr/share/man/man8

	$(INSTALL_DATA) $(PKG_BUILD_DIR)/*.8 \
		$(1)/usr/share/man/man8/ 2>/dev/null || true
endef


$(eval $(call BuildPackage,dsniff))
