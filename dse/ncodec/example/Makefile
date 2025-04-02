# Copyright 2023 Robert Bosch GmbH
#
# SPDX-License-Identifier: Apache-2.0

GCC_BUILDER_IMAGE ?= ghcr.io/boschglobal/dse-gcc-builder:main


default: build_docker

.PHONY: all
all: build
	cd build; make

build:
	mkdir build;
	cd build; cmake ..

.PHONY: build_docker
build_docker:
	@docker run -it --rm \
		--volume $$(pwd)/../../..:/tmp/repo \
		--workdir /tmp/repo/dse/ncodec/example \
		--env PACKAGE_ARCH=$(PACKAGE_ARCH) \
		--env CMAKE_TOOLCHAIN_FILE=/tmp/repo/dse/ncodec/example/$(PACKAGE_ARCH).cmake \
		$(GCC_BUILDER_IMAGE) \
		/bin/bash -c "make all"

.PHONY: clean
clean:
	rm -rf build
