.PHONY: rocketchat-help rocketchat-up rocketchat-down rocketchat-restart rocketchat-logs rocketchat-status rocketchat-shell rocketchat-clean rocketchat-pull rocketchat-update

ROCKETCHAT_DIR := $(dir $(abspath $(lastword $(MAKEFILE_LIST))))

rocketchat-help: ## Show Rocket.Chat commands
	@echo "Rocket.Chat Commands:"
	@grep -E '^rocketchat-[a-zA-Z_-]+:.*?## .*$$' $(ROCKETCHAT_DIR)Makefile | awk 'BEGIN {FS = ":.*?## "}; {printf "  %-25s %s\n", $$1, $$2}'

rocketchat-up: ## Start Rocket.Chat
	@echo "Starting Rocket.Chat..."
	@cd $(ROCKETCHAT_DIR) && docker compose up -d
	@echo "Rocket.Chat is running!"

rocketchat-down: ## Stop Rocket.Chat
	@echo "Stopping Rocket.Chat..."
	@cd $(ROCKETCHAT_DIR) && docker compose down
	@echo "Rocket.Chat stopped"

rocketchat-restart: ## Restart Rocket.Chat
	@echo "Restarting Rocket.Chat..."
	@cd $(ROCKETCHAT_DIR) && docker compose restart
	@echo "Rocket.Chat restarted"

rocketchat-logs: ## Show Rocket.Chat logs
	@cd $(ROCKETCHAT_DIR) && docker compose logs -f

rocketchat-status: ## Show Rocket.Chat status
	@cd $(ROCKETCHAT_DIR) && docker compose ps

rocketchat-shell: ## Open shell in Rocket.Chat container
	@cd $(ROCKETCHAT_DIR) && docker compose exec rocketchat sh

rocketchat-clean: ## Remove Rocket.Chat containers and volumes
	@echo "WARNING: This will remove all Rocket.Chat data!"
	@printf "Are you sure? [y/N] "; \
	read -r reply; \
	case "$$reply" in \
		[Yy]*) cd $(ROCKETCHAT_DIR) && docker compose down -v; echo "Rocket.Chat cleaned";; \
		*) echo "Canceled";; \
	esac

rocketchat-pull: ## Pull latest Rocket.Chat image
	@echo "Pulling latest Rocket.Chat image..."
	@cd $(ROCKETCHAT_DIR) && docker compose pull
	@echo "Pull complete!"

rocketchat-update: ## Update Rocket.Chat to latest version
	@echo "Updating Rocket.Chat..."
	@cd $(ROCKETCHAT_DIR) && docker compose pull
	@cd $(ROCKETCHAT_DIR) && docker compose up -d
	@echo "Rocket.Chat updated!"
