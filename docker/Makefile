NAME := advent

xlist = alpine \
				bionic \
				buster \
				KNUT0350 \
				WOOD0430 \
				LUPI0440 \
				PLAT0550 \
				HALL0501 \
				MCDO0551

.PHONY: all name build cloud-build clean tag push $(xlist)

all: build

$(xlist):
	cd $(NAME)/$@ \
	&& $(MAKE) build

clean:
	cd $(NAME) \
	&& $(MAKE) clean

tag:
	cd $(NAME) \
	&& $(MAKE) tag

push:
	cd $(NAME) \
	&& $(MAKE) push

git-deps:
	cd $(NAME) \
	&& $(MAKE) git-deps

cloud-prep:
	cd $(NAME) \
	&& mv ../adaar-apps . \
	&& mv ../perlibs . \
	&& $(MAKE) cloud-build

cloud-build: $(xlist)

test:
	cd $(NAME) \
	&& $(MAKE) test

build:
	cd $(NAME) \
	&& $(MAKE)
