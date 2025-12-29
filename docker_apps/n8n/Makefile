.PHONY: n8n-help n8n-up n8n-down n8n-restart n8n-logs n8n-status n8n-shell n8n-clean n8n-pull n8n-update

N8N_DIR := $(dir $(abspath $(lastword $(MAKEFILE_LIST))))

n8n-help: ## Show n8n commands
	@echo "n8n Commands:"
	@grep -E '^n8n-[a-zA-Z_-]+:.*?## .*$$' $(N8N_DIR)Makefile | awk 'BEGIN {FS = ":.*?## "}; {printf "  %-25s %s\n", $$1, $$2}'

n8n-up: ## Start n8n
	@echo "Starting n8n..."
	@cd $(N8N_DIR) && docker compose up -d
	@echo "n8n is running!"

n8n-down: ## Stop n8n
	@echo "Stopping n8n..."
	@cd $(N8N_DIR) && docker compose down
	@echo "n8n stopped"

n8n-restart: ## Restart n8n
	@echo "Restarting n8n..."
	@cd $(N8N_DIR) && docker compose restart
	@echo "n8n restarted"

n8n-logs: ## Show n8n logs
	@cd $(N8N_DIR) && docker compose logs -f

n8n-status: ## Show n8n status
	@cd $(N8N_DIR) && docker compose ps

n8n-shell: ## Open shell in n8n container
	@cd $(N8N_DIR) && docker compose exec n8n sh

n8n-clean: ## Remove n8n containers and volumes
	@echo "WARNING: This will remove all n8n data!"
	@printf "Are you sure? [y/N] "; \
	read -r reply; \
	case "$$reply" in \
		[Yy]*) cd $(N8N_DIR) && docker compose down -v; echo "n8n cleaned";; \
		*) echo "Canceled";; \
	esac

n8n-pull: ## Pull latest n8n images
	@echo "Pulling latest n8n images..."
	@cd $(N8N_DIR) && docker compose pull
	@echo "Pull complete!"

n8n-update: ## Update n8n to latest version
	@echo "Updating n8n..."
	@cd $(N8N_DIR) && docker compose pull
	@cd $(N8N_DIR) && docker compose up -d
	@echo "n8n updated!"
