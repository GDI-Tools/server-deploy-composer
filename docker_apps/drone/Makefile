.PHONY: drone-help drone-up drone-down drone-restart drone-logs drone-logs-server drone-logs-runner drone-status drone-clean drone-shell-server drone-shell-runner

DRONE_DIR := $(dir $(abspath $(lastword $(MAKEFILE_LIST))))

drone-help: ## Show Drone commands
	@echo "Drone CI Commands:"
	@grep -E '^drone-[a-zA-Z_-]+:.*?## .*$$' $(DRONE_DIR)Makefile | awk 'BEGIN {FS = ":.*?## "}; {printf "  %-25s %s\n", $$1, $$2}'

drone-up: ## Start Drone CI
	@echo "Starting Drone CI..."
	@cd $(DRONE_DIR) && docker compose up -d
	@echo "Drone CI is running!"

drone-down: ## Stop Drone CI
	@echo "Stopping Drone CI..."
	@cd $(DRONE_DIR) && docker compose down
	@echo "Drone CI stopped"

drone-restart: ## Restart Drone CI
	@echo "Restarting Drone CI..."
	@cd $(DRONE_DIR) && docker compose restart
	@echo "Drone CI restarted"

drone-logs: ## Show all Drone logs
	@cd $(DRONE_DIR) && docker compose logs -f

drone-logs-server: ## Show Drone server logs
	@cd $(DRONE_DIR) && docker compose logs -f drone-server

drone-logs-runner: ## Show Drone runner logs
	@cd $(DRONE_DIR) && docker compose logs -f drone-runner

drone-status: ## Show Drone status
	@cd $(DRONE_DIR) && docker compose ps

drone-shell-server: ## Open shell in Drone server
	@cd $(DRONE_DIR) && docker compose exec drone-server sh

drone-shell-runner: ## Open shell in Drone runner
	@cd $(DRONE_DIR) && docker compose exec drone-runner sh

drone-clean: ## Remove Drone containers and volumes
	@echo "WARNING: This will remove all Drone data!"
	@printf "Are you sure? [y/N] "; \
	read -r reply; \
	case "$$reply" in \
		[Yy]*) cd $(DRONE_DIR) && docker compose down -v; echo "Drone CI cleaned";; \
		*) echo "Canceled";; \
	esac

drone-pull: ## Pull latest Drone images
	@echo "Pulling latest Drone images..."
	@cd $(DRONE_DIR) && docker compose pull
	@echo "Pull complete!"

drone-update: ## Update Drone to latest version
	@echo "Updating Drone..."
	@cd $(DRONE_DIR) && docker compose pull
	@cd $(DRONE_DIR) && docker compose up -d
	@echo "Drone updated!"
