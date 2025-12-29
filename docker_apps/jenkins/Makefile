.PHONY: jenkins-help jenkins-up jenkins-down jenkins-restart jenkins-logs jenkins-status jenkins-shell jenkins-clean jenkins-pull jenkins-update

JENKINS_DIR := $(dir $(abspath $(lastword $(MAKEFILE_LIST))))

jenkins-help: ## Show Jenkins commands
	@echo "Jenkins Commands:"
	@grep -E '^jenkins-[a-zA-Z_-]+:.*?## .*$$' $(JENKINS_DIR)Makefile | awk 'BEGIN {FS = ":.*?## "}; {printf "  %-25s %s\n", $$1, $$2}'

jenkins-up: ## Start Jenkins
	@echo "Starting Jenkins..."
	@cd $(JENKINS_DIR) && docker compose up -d
	@echo "Jenkins is running!"

jenkins-down: ## Stop Jenkins
	@echo "Stopping Jenkins..."
	@cd $(JENKINS_DIR) && docker compose down
	@echo "Jenkins stopped"

jenkins-restart: ## Restart Jenkins
	@echo "Restarting Jenkins..."
	@cd $(JENKINS_DIR) && docker compose restart
	@echo "Jenkins restarted"

jenkins-logs: ## Show Jenkins logs
	@cd $(JENKINS_DIR) && docker compose logs -f

jenkins-status: ## Show Jenkins status
	@cd $(JENKINS_DIR) && docker compose ps

jenkins-shell: ## Open shell in Jenkins container
	@cd $(JENKINS_DIR) && docker compose exec jenkins bash

jenkins-clean: ## Remove Jenkins containers and volumes
	@echo "WARNING: This will remove all Jenkins data!"
	@printf "Are you sure? [y/N] "; \
	read -r reply; \
	case "$$reply" in \
		[Yy]*) cd $(JENKINS_DIR) && docker compose down -v; echo "Jenkins cleaned";; \
		*) echo "Canceled";; \
	esac

jenkins-pull: ## Pull latest Jenkins image
	@echo "Pulling latest Jenkins image..."
	@cd $(JENKINS_DIR) && docker compose pull
	@echo "Pull complete!"

jenkins-update: ## Update Jenkins to latest version
	@echo "Updating Jenkins..."
	@cd $(JENKINS_DIR) && docker compose pull
	@cd $(JENKINS_DIR) && docker compose up -d
	@echo "Jenkins updated!"
