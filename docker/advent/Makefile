NAME := $(notdir $(CURDIR))
REPO := magicjuan
target_dir = $(shell pwd)
INTERACTIVE:=$(shell [ -t 0 ] && echo -it)

xlist = alpine \
				bionic \
				buster \
				KNUT0350 \
				WOOD0430 \
				LUPI0440 \
				PLAT0550 \
				HALL0501 \
				MCDO0551

.PHONY: all name build cloud-build clean test $(xlist)

all: build

clean:
	rm -rf alpine/builder
	rm -rf bionic/builder
	rm -rf buster/builder

tag:
	cd alpine; $(MAKE) tag
	cd bionic; $(MAKE) tag
	cd buster; $(MAKE) tag
	cd KNUT0350; $(MAKE) tag
	cd WOOD0430; $(MAKE) tag
	cd LUPI0440; $(MAKE) tag
	cd PLAT0550; $(MAKE) tag
	cd HALL0501; $(MAKE) tag
	cd MCDO0551; $(MAKE) tag

push:
	cd alpine; $(MAKE) push
	cd bionic; $(MAKE) push
	cd buster; $(MAKE) push
	cd KNUT0350; $(MAKE) push push-latest
	cd WOOD0430; $(MAKE) push
	cd LUPI0440; $(MAKE) push
	cd PLAT0550; $(MAKE) push
	cd HALL0501; $(MAKE) push
	cd MCDO0551; $(MAKE) push

name:
	@echo $(NAME)

pkg:

$(xlist):
	cd $@ \
	&& $(MAKE) build

build: $(xlist)
	@echo done.

cloud-build:
	@echo done.

test:
	@echo "====> NO TESTS DEFINED <===="
