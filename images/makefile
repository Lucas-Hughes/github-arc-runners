# Define variables for Docker image names and versions
REPO_NAME := lucasjhughes
PLATFORM := linux/amd64
VERSION ?= latest

# Default target
all: base kaniko

# Target for building the base Docker image
base:
	docker buildx build --platform $(PLATFORM) -t $(REPO_NAME)/base-arc-runner:$(VERSION) --push -f base/dockerfile .

# Target for building the Kaniko Docker image 
kaniko:
	docker buildx build --platform $(PLATFORM) -t $(REPO_NAME)/kaniko-arc-runner:$(VERSION) --push -f kaniko/dockerfile .

.PHONY: all base kaniko clean
