
# SPDX-License-Identifier: GPL-2.0
#
# Copyright (c) 2011, 2018, Oracle and/or its affiliates. All rights reserved.
#
# Implementation of the kernel part of Kernel Test Framework (KTF),
# a framework for running unit test like tests within the kernel.
#

obj-m += ktf.o

-include ktf_gen.mk

ktf-y := ktf_context.o ktf_nl.o ktf_map.o ktf_test.o ktf_debugfs.o ktf_cov.o \
	 ktf_override.o ktf_netctx.o ktf_kallsyms.o

all:
	$(MAKE) -C $(KERNEL_SRC) ARCH=$(ARCH) M=$(shell pwd) $(filter-out all,$(MAKECMDGOALS))

clean:
	rm -Rf Module.symvers *.o *.ko modules.order .*.cmd .tmp_versions *.mod.c
