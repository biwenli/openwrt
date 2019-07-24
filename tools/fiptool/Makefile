#
# Copyright (C) 2019 NXP
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=fiptool
PKG_VERSION:=lsdk-1903

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://source.codeaurora.org/external/qoriq/qoriq-components/atf
PKG_SOURCE_VERSION:=7e34aebe658c7c3439d2d68b0ce6b9776e8e6996
PKG_MIRROR_HASH:=9cf0bc32fa589a0ee7c48c87898679e645341f29da1253d0ba5d2e82c6ea074d
HOST_BUILD_DIR:=$(BUILD_DIR_HOST)/$(PKG_NAME)-$(PKG_VERSION)
HOST_FIPTOOL_BUILD_DIR:=$(HOST_BUILD_DIR)/tools/fiptool

HOST_BUILD_PARALLEL:=1

HOST_LDFLAGS:= -static -L$(STAGING_DIR_HOST)/lib -lcrypto

override HOST_CPPFLAGS:= -D_GNU_SOURCE -D_XOPEN_SOURCE=700

HOST_CFLAGS:= -Wall -Werror -pedantic -std=c99
HOST_CFLAGS+= -I$(STAGING_DIR_HOST)/include

INCLUDE_PATHS:= -I$(HOST_BUILD_DIR)/include/tools_share

HOSTCC:=$(STAGING_DIR_HOST)/bin/gcc

include $(INCLUDE_DIR)/host-build.mk

define Host/Prepare
	$(Host/Prepare/Default)
endef

define Host/Compile
	$(HOSTCC) -o $(HOST_FIPTOOL_BUILD_DIR)/fiptool $(HOST_FIPTOOL_BUILD_DIR)/fiptool.c $(HOST_FIPTOOL_BUILD_DIR)/tbbr_config.c $(HOST_CPPFLAGS) $(HOST_CFLAGS) $(HOST_LDFLAGS) $(INCLUDE_PATHS)
endef

define Host/Install
	$(CP) $(HOST_FIPTOOL_BUILD_DIR)/fiptool $(STAGING_DIR_HOST)/bin/
endef

define Host/Clean
	rm -f $(STAGING_DIR_HOST)/bin/fiptool
endef

$(eval $(call HostBuild))
