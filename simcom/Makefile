include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk
 
PKG_NAME:=simcom_wwan
PKG_VERSION:=V1.00-20160822
PKG_RELEASE:=1
 
include $(INCLUDE_DIR)/package.mk
 
define KernelPackage/$(PKG_NAME)
  SUBMENU:=Other modules
  TITLE:=This is a $(PKG_NAME) driver
  DEPENDS:=+kmod-usb-net +kmod-usb-serial +kmod-usb-serial-option
  FILES:=$(PKG_BUILD_DIR)/$(PKG_NAME).ko
  AUTOLOAD:=$(call AutoProbe,$(PKG_NAME)) #AutoProbe  #AutoLoad
  KCONFIG:=
endef
 
define KernelPackage/$(PKG_NAME)/description
	This is a $(PKG_NAME) device.
endef
 
EXTRA_KCONFIG:= \
		CONFIG_SIMCOM_WWAN=m

EXTRA_CFLAGS:= \
        $(patsubst CONFIG_%, -DCONFIG_%=1, $(patsubst %=m,%,$(filter %=m,$(EXTRA_KCONFIG)))) \
        $(patsubst CONFIG_%, -DCONFIG_%=1, $(patsubst %=y,%,$(filter %=y,$(EXTRA_KCONFIG)))) \
 
MAKE_OPTS:= \
	$(KERNEL_MAKE_FLAGS) \
	SUBDIRS="$(PKG_BUILD_DIR)" \
	EXTRA_CFLAGS="$(EXTRA_CFLAGS)" \
	$(EXTRA_KCONFIG)

define Build/Compile
	$(MAKE) -C "$(LINUX_DIR)" \
		$(MAKE_OPTS) \
		modules
endef

 
$(eval $(call KernelPackage,$(PKG_NAME)))
