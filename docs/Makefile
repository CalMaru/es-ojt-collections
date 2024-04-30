.DEFAULT_GOAL:=help

COMPOSE := -f docker-compose.yml

compose_v2_not_supported = $(shell command docker compose 2> /dev/null)
ifeq (,$(compose_v2_not_supported))
	DOCKER_COMPOSE_COMMAND = docker-compose
else
	DOCKER_COMPOSE_COMMAND = docker compose
endif

ifdef build
	BUILD_COMMAND = npm run build
else
	BUILD_COMMAND = @echo "skip build"
endif

# --------------------------
.PHONY: start docs down stop help

start: ## npm run start es-ojt docs.
	npm run start

docs: ## Start es-ojt docs container.
	$(BUILD_COMMAND)
	$(DOCKER_COMPOSE_COMMAND) up -d

down: ## Down es-ojt docs and all its extra components.
	$(DOCKER_COMPOSE_COMMAND) ${COMPOSE} down

stop: ## Stop es-ojt docs and all its extra components.
	$(DOCKER_COMPOSE_COMMAND) ${COMPOSE} stop

help: ## Show this help.
	@echo "Make es-ojt docs with docker-compose files"
	@awk 'BEGIN {FS = ":.*##"; printf "\nUsage:\n  make \033[36m<target>\033[0m (default: help)\n\nTargets:\n"} /^[a-zA-Z_-]+:.*?##/ { printf "  \033[36m%-12s\033[0m %s\n", $$1, $$2 }' $(MAKEFILE_LIST)