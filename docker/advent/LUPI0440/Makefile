SELF_DIR := $(dir $(lastword $(CURDIR)))
NAME := $(notdir $(notdir $(patsubst %/,%,$(SELF_DIR))))
VERSION := $(notdir $(CURDIR))
REPO := magicjuan
target_dir = $(shell pwd)
PARENT_IMAGE = alpine
ADVENT_VERSION= $(shell echo $(VERSION) | sed -e 's/^[A-Z,a-z]*//' | sed -e 's/^0*//')

.PHONY: all cloud-build build tag test run run-it history tag-latest push-latest push

all: build

cloud-build:
	@echo Ready to build docker $(NAME):$(VERSION)

build-parent-image:
	cd ../$(PARENT_IMAGE); $(MAKE)

build: build-parent-image
	docker build -t $(NAME):$(VERSION) --rm .

tag:
	docker tag $(NAME):$(VERSION) $(REPO)/$(NAME):$(VERSION)
	docker tag $(NAME):$(VERSION) $(REPO)/$(NAME):$(ADVENT_VERSION)

push: tag
	docker push $(REPO)/$(NAME):$(VERSION)
	docker push $(REPO)/$(NAME):$(ADVENT_VERSION)

test: build
	docker run \
		-it --rm $(NAME):$(VERSION) $(RUN_ARGS) perl test.pl

run:
	docker run \
		-it --rm $(NAME):$(VERSION) $(RUN_ARGS)

run-it:
	docker run \
		-it --rm $(NAME):$(VERSION) $(RUN_ARGS) sh

history:
	docker history $(NAME):$(VERSION)

tag-latest:
	docker tag $(NAME):$(VERSION) $(REPO)/$(NAME):latest

push-latest: tag-latest
	docker push $(REPO)/$(NAME):latest
