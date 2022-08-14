obj-m += ktf.o
ktf-y := ktf_context.o ktf_nl.o ktf_map.o ktf_test.o ktf_debugfs.o ktf_cov.o

all:
	$(MAKE) -C $(KERNEL_SRC) ARCH=$(ARCH) CROSS_COMPILE=$(CROSS_COMPILE) M=$(shell pwd) $(filter-out all,$(MAKECMDGOALS))

clean:
	rm -Rf Module.symvers *.o *.ko modules.order .*.cmd .tmp_versions *.mod.c
