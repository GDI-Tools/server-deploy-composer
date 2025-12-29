.PHONY: portainer-help portainer-up portainer-down portainer-restart portainer-logs portainer-status portainer-shell portainer-clean portainer-pull portainer-update

PORTAINER_DIR := $(dir $(abspath $(lastword $(MAKEFILE_LIST))))

portainer-help: ## Show Portainer commands
	@echo "Portainer Commands:"
	@grep -E '^portainer-[a-zA-Z_-]+:.*?## .*$$' $(PORTAINER_DIR)Makefile | awk 'BEGIN {FS = ":.*?## "}; {printf "  %-25s %s\n", $$1, $$2}'

portainer-up: ## Start Portainer
	@echo "Starting Portainer..."
	@cd $(PORTAINER_DIR) && docker compose up -d
	@echo "Portainer is running!"

portainer-down: ## Stop Portainer
	@echo "Stopping Portainer..."
	@cd $(PORTAINER_DIR) && docker compose down
	@echo "Portainer stopped"

portainer-restart: ## Restart Portainer
	@echo "Restarting Portainer..."
	@cd $(PORTAINER_DIR) && docker compose restart
	@echo "Portainer restarted"

portainer-logs: ## Show Portainer logs
	@cd $(PORTAINER_DIR) && docker compose logs -f

portainer-status: ## Show Portainer status
	@cd $(PORTAINER_DIR) && docker compose ps

portainer-shell: ## Open shell in Portainer container
	@cd $(PORTAINER_DIR) && docker compose exec portainer sh

portainer-clean: ## Remove Portainer containers and volumes
	@echo "WARNING: This will remove all Portainer data!"
	@printf "Are you sure? [y/N] "; \
	read -r reply; \
	case "$$reply" in \
		[Yy]*) cd $(PORTAINER_DIR) && docker compose down -v; echo "Portainer cleaned";; \
		*) echo "Canceled";; \
	esac

portainer-pull: ## Pull latest Portainer image
	@echo "Pulling latest Portainer image..."
	@cd $(PORTAINER_DIR) && docker compose pull
	@echo "Pull complete!"

portainer-update: ## Update Portainer to latest version
	@echo "Updating Portainer..."
	@cd $(PORTAINER_DIR) && docker compose pull
	@cd $(PORTAINER_DIR) && docker compose up -d
	@echo "Portainer updated!"
