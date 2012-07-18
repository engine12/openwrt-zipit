#
# Copyright (C) 2008-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/image.mk

CUSTOM_MODULES=$(TOPDIR)/files/lib/modules/

define Image/Prepare
#	echo Image/Prepare/TARGET_DIR: $(TARGET_DIR)
	rm -rf $(TARGET_DIR)/lib/modules/*
	cp -r $(CUSTOM_MODULES) $(TARGET_DIR)/lib/
	cp $(LINUX_DIR)/arch/arm/boot/uImage $(KDIR)/uImage
	
#	read -n 1 -p "....press any key to continue"
endef

define Image/BuildKernel
	cp $(KDIR)/uImage $(BIN_DIR)/$(IMG_PREFIX)-uImage
endef

define Image/Build
	$(call Image/Build/$(1),$(1))
endef

define Image/Build/jffs2-64k
	dd if=$(KDIR)/root.$(1) of=$(BIN_DIR)/$(IMG_PREFIX)-$(1).img bs=64k conv=sync
endef

define Image/Build/jffs2-128k
	dd if=$(KDIR)/root.$(1) of=$(BIN_DIR)/$(IMG_PREFIX)-$(1).img bs=128k conv=sync
endef

define Image/Build/squashfs
	$(call prepare_generic_squashfs,$(KDIR)/root.squashfs)
	dd if=$(KDIR)/root.$(1) of=$(BIN_DIR)/$(IMG_PREFIX)-$(1).img bs=128k conv=sync
endef

$(eval $(call BuildImage))
