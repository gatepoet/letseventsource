SHELL := /bin/bash
APPLICATION_NAME ?= docs
APPLICATION_DIRECTORY ?= .
ORGANIZATION ?= les
VERSION ?= `date '+%Y-%m-%d-'``git show -s --format='commit-%h'`
DOCKER_REPO ?= adaptech.azurecr.io
APPLICATION_FQDN ?= letseventsource.net

.PHONY: all
all: build-web-container

.PHONY: build-web
build-web:
	cd $(APPLICATION_DIRECTORY) \
	&& hugo

.PHONY: build-web-container
build-web-container: build-web
	docker build -t $(DOCKER_REPO)/$(ORGANIZATION)-$(APPLICATION_NAME)-web:$(VERSION) $(APPLICATION_DIRECTORY) \
	&& docker tag $(DOCKER_REPO)/$(ORGANIZATION)-$(APPLICATION_NAME)-web:$(VERSION) $(DOCKER_REPO)/$(ORGANIZATION)-$(APPLICATION_NAME)-web:latest

.PHONY: push-web-container
push-web-container:
	docker push $(DOCKER_REPO)/$(ORGANIZATION)-$(APPLICATION_NAME)-web:$(VERSION) \
	&& docker push $(DOCKER_REPO)/$(ORGANIZATION)-$(APPLICATION_NAME)-web:latest

