.PHONY: nextcloud-help nextcloud-up nextcloud-down nextcloud-restart nextcloud-logs nextcloud-status nextcloud-shell nextcloud-clean nextcloud-pull nextcloud-update

NEXTCLOUD_DIR := $(dir $(abspath $(lastword $(MAKEFILE_LIST))))

nextcloud-help: ## Show Nextcloud commands
	@echo "Nextcloud Commands:"
	@grep -E '^nextcloud-[a-zA-Z_-]+:.*?## .*$$' $(NEXTCLOUD_DIR)Makefile | awk 'BEGIN {FS = ":.*?## "}; {printf "  %-25s %s\n", $$1, $$2}'

nextcloud-up: ## Start Nextcloud
	@echo "Starting Nextcloud..."
	@cd $(NEXTCLOUD_DIR) && docker compose up -d
	@echo "Nextcloud is running!"

nextcloud-down: ## Stop Nextcloud
	@echo "Stopping Nextcloud..."
	@cd $(NEXTCLOUD_DIR) && docker compose down
	@echo "Nextcloud stopped"

nextcloud-restart: ## Restart Nextcloud
	@echo "Restarting Nextcloud..."
	@cd $(NEXTCLOUD_DIR) && docker compose restart
	@echo "Nextcloud restarted"

nextcloud-logs: ## Show Nextcloud logs
	@cd $(NEXTCLOUD_DIR) && docker compose logs -f

nextcloud-status: ## Show Nextcloud status
	@cd $(NEXTCLOUD_DIR) && docker compose ps

nextcloud-shell: ## Open shell in Nextcloud container
	@cd $(NEXTCLOUD_DIR) && docker compose exec nextcloud bash

nextcloud-clean: ## Remove Nextcloud containers and volumes
	@echo "WARNING: This will remove all Nextcloud data!"
	@printf "Are you sure? [y/N] "; \
	read -r reply; \
	case "$$reply" in \
		[Yy]*) cd $(NEXTCLOUD_DIR) && docker compose down -v; echo "Nextcloud cleaned";; \
		*) echo "Canceled";; \
	esac

nextcloud-pull: ## Pull latest Nextcloud image
	@echo "Pulling latest Nextcloud image..."
	@cd $(NEXTCLOUD_DIR) && docker compose pull
	@echo "Pull complete!"

nextcloud-update: ## Update Nextcloud to latest version
	@echo "Updating Nextcloud..."
	@cd $(NEXTCLOUD_DIR) && docker compose pull
	@cd $(NEXTCLOUD_DIR) && docker compose up -d
	@echo "Nextcloud updated!"
