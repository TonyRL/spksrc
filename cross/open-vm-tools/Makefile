PKG_NAME = open-vm-tools
PKG_VERS = 10.1.15
PKG_BUILD = 6677369
PKG_EXT = tar.gz
PKG_DIST_FILE = $(PKG_NAME)-$(PKG_VERS)-$(PKG_BUILD).$(PKG_EXT)
PKG_DIST_NAME = $(PKG_DIST_FILE)
PKG_DIST_SITE = https://github.com/vmware/open-vm-tools/releases/download/stable-$(PKG_VERS)
PKG_DIR = $(PKG_NAME)-$(PKG_VERS)-$(PKG_BUILD)

DEPENDS = cross/glib cross/openssl cross/procps-ng cross/fuse cross/libdnet cross/libtirpc cross/libmspack

HOMEPAGE = https://github.com/vmware/open-vm-tools
COMMENT  = open-vm-tools is a set of services and modules that enable several features in VMware products for better management of, and seamless user interactions with, guests
LICENSE  = GPLv2

PRE_CONFIGURE_TARGET = myPreConfigure
INSTALL_TARGET = myInstall

ENV += CUSTOM_PROCPS_NAME=procps
ENV += CUSTOM_PROCPS_LIBS="-L$(STAGING_INSTALL_PREFIX)/lib -lprocps"
ADDITIONAL_CFLAGS = -Wno-error -Dlinux=1 -Wno-implicit-function-declaration
ADDITIONAL_LDFLAGS = -L$(STAGING_INSTALL_PREFIX)/lib64 -Wl,--rpath-link,$(STAGING_INSTALL_PREFIX)/lib64 -Wl,--rpath,$(INSTALL_PREFIX)/lib64
ADDITIONAL_CXXFLAGS = -std=c++11
ENV += PATH=$(STAGING_INSTALL_PREFIX)/bin:$$PATH

PATCHES_LEVEL = 2

GNU_CONFIGURE = 1
CONFIGURE_ARGS = --with-dnet
CONFIGURE_ARGS += --enable-deploypkg
CONFIGURE_ARGS += --without-kernel-modules
# CONFIGURE_ARGS += --without-root-privileges
CONFIGURE_ARGS += --without-pam
CONFIGURE_ARGS += --without-xmlsecurity
CONFIGURE_ARGS += --without-xerces
CONFIGURE_ARGS += --without-x
CONFIGURE_ARGS += --without-icu

include ../../mk/spksrc.cross-cc.mk

myPreConfigure:
	$(RUN) autoreconf -fiv
myInstall:
	$(RUN) $(MAKE) install prefix=$(STAGING_INSTALL_PREFIX) confdir=$(STAGING_INSTALL_PREFIX)/etc/vmware-tools
