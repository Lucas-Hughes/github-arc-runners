# Variables
NAMESPACE_ARC_SYSTEMS := arc-systems
NAMESPACE_ARC_RUNNERS := arc-runners
ARC_VALUES_FILE := arc-controller-values.yaml
RUNNER_SET_VALUES_FILE := helm-base.yaml
KANIKO_SET_VALUES_FILE := helm-kaniko.yaml
DIND_SET_VALUES_FILE := helm-dind.yaml
ARC_CHART_URL := oci://ghcr.io/actions/actions-runner-controller-charts/gha-runner-scale-set-controller
RUNNER_SET_CHART_URL := oci://ghcr.io/actions/actions-runner-controller-charts/gha-runner-scale-set

# Default target
.PHONY: all
all: install-arc install-runner-set

## ARC CONTROLLER ##

# Install ARC helm chart
.PHONY: install-arc
install-arc:
	helm install arc --namespace $(NAMESPACE_ARC_SYSTEMS) -f $(ARC_VALUES_FILE) $(ARC_CHART_URL)

# Upgrade ARC helm deployment
.PHONY: upgrade-arc
upgrade-arc:
	helm upgrade arc --namespace $(NAMESPACE_ARC_SYSTEMS) -f $(ARC_VALUES_FILE) $(ARC_CHART_URL)

# Uninstall ARC helm chart
.PHONY: uninstall-arc
uninstall-arc:
	helm uninstall arc -n $(NAMESPACE_ARC_SYSTEMS)

### ARC SCALE SETS ###

## Base ##

# Install ARC runner set
.PHONY: install-runner-set
install-runner-set:
	helm install arc-runner-set --namespace $(NAMESPACE_ARC_RUNNERS) -f $(RUNNER_SET_VALUES_FILE) $(RUNNER_SET_CHART_URL)

# Upgrade ARC runner set
.PHONY: upgrade-runner-set
upgrade-runner-set:
	helm upgrade arc-runner-set $(RUNNER_SET_CHART_URL) --namespace $(NAMESPACE_ARC_RUNNERS) -f $(RUNNER_SET_VALUES_FILE)

# Uninstall ARC runner set
.PHONY: uninstall-runner-set
uninstall-runner-set:
	helm uninstall arc-runner-set --namespace $(NAMESPACE_ARC_RUNNERS)

## Kaniko ##

.PHONY: install-kaniko-set
install-kaniko-set:
	helm install kaniko-runner-set --namespace $(NAMESPACE_ARC_RUNNERS) -f $(KANIKO_SET_VALUES_FILE) $(RUNNER_SET_CHART_URL)

# Upgrade ARC runner set
.PHONY: upgrade-kaniko-set
upgrade-kaniko-set:
	helm upgrade kaniko-runner-set $(RUNNER_SET_CHART_URL) --namespace $(NAMESPACE_ARC_RUNNERS) -f $(KANIKO_SET_VALUES_FILE)

# Uninstall ARC runner set
.PHONY: uninstall-kaniko-set
uninstall-kaniko-set:
	helm uninstall kaniko-runner-set --namespace $(NAMESPACE_ARC_RUNNERS)

## DinD ##
# install DinD runner set
.PHONY: install-dind-set
install-dind-set:
	helm install dind-runner-set --namespace $(NAMESPACE_ARC_RUNNERS) -f $(DIND_SET_VALUES_FILE) $(RUNNER_SET_CHART_URL)

# Upgrade dind runner set
.PHONY: upgrade-dind-set
upgrade-dind-set:
	helm upgrade dind-runner-set $(RUNNER_SET_CHART_URL) --namespace $(NAMESPACE_ARC_RUNNERS) -f $(DIND_SET_VALUES_FILE)

# Uninstall dind runner set
.PHONY: uninstall-dind-set
uninstall-dind-set:
	helm uninstall dind-runner-set --namespace $(NAMESPACE_ARC_RUNNERS)

# Help
.PHONY: help
help:
	@echo "Usage:"
	@echo "  make [target]"
	@echo "Targets:"
	@echo "  install-arc             Install the ARC helm chart."
	@echo "  upgrade-arc             Upgrade the ARC helm deployment."
	@echo "  uninstall-arc           Uninstall the ARC helm chart."
	@echo "  install-runner-set      Install the ARC runner set."
	@echo "  upgrade-runner-set      Upgrade the ARC runner set helm deployment."
	@echo "  uninstall-runner-set    Uninstall the ARC runner set."
	@echo "  annotate-service-account Annotate the Kubernetes service account for ARC."
	@echo "  label-namespace-arc-systems Label namespace for Anthos/Istio for arc-systems."
	@echo "  label-namespace-arc-runners Label namespace for Anthos/Istio for arc-runners."
