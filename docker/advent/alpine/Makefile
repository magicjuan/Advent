SELF_DIR := $(dir $(lastword $(CURDIR)))
NAME := $(notdir $(notdir $(patsubst %/,%,$(SELF_DIR))))
VERSION := $(notdir $(CURDIR))
REPO := magicjuan
target_dir = $(shell pwd)
DEFAULT_SHELL = sh

.PHONY: all cloud-build build tag test run run-it history tag-latest push-latest push

all: build

cloud-build:
	@echo Ready to build docker $(NAME):$(VERSION)

builder:
	mkdir builder

builder/Makefile: builder
	cp ../../template/Makefile-advent builder/Makefile

builder/src.tgz: builder ../../../KNUT0350 ../../../WOOD0430 ../../../LUPI0440 ../../../HALL0501 ../../../PLAT0550 ../../../MCDO0551
	tar -cvzf builder/src.tgz  -C ../../.. KNUT0350 WOOD0430 LUPI0440 HALL0501 PLAT0550 MCDO0551

build: builder builder/Makefile builder/src.tgz
	# to show full output run instead:
	#   docker build -t $(NAME):$(VERSION) --progress=plain --rm .
	docker build -t $(NAME):$(VERSION) --rm .

tag:
	docker tag $(NAME):$(VERSION) $(REPO)/$(NAME):$(VERSION)
	#docker push $(REPO)/$(NAME):$(VERSION)

push: tag
	docker push $(REPO)/$(NAME):$(VERSION)

test: build
	docker run \
		-it --rm $(NAME):$(VERSION) $(RUN_ARGS) perl test.pl

run:
	docker run \
		-it --rm $(NAME):$(VERSION) $(RUN_ARGS)

run-it:
	docker run \
		-it --rm $(NAME):$(VERSION) $(RUN_ARGS) $(DEFAULT_SHELL)

history:
	docker history $(NAME):$(VERSION)

tag-latest:
	docker tag  $(NAME):$(VERSION) $(NAME):latest


push-latest:
	docker push  $(NAME):$(VERSION) $(NAME):latest
