# GitHub Arc Runners

This project facilitates the creation and deployment of a GitHub Arc Runner Controller and Arc-Runner-Sets at the organizational or repository level. It includes a Helm chart with deployment commands to install in one's Kubernetes cluster, Docker images used inside the scale sets, and Kubernetes manifests to create the necessary components.

## Prerequisites

### Software:
- kubernetes/kubectl
- helm
- docker
- make
  
### Kubernetes infra:
- A kubernetes cluster
- Namespaces for the `arc-systems` and `arc-runners` - this can be customized to whatever you need, including one per scale set. The `github-app.yaml/github-pat.yaml` used in the `helm-*.yaml` must be in the same namespace as secrets are namespaced resources
  
## Quickstart
If you care less about what is involved in the project and want a quick guide to getting the ARC runners up and going, follow these steps:
   - Once cloned/copied, navigate to the `./quickstart` directory
   - Create a OAuth app or Personal Access token with proper permissions - https://github.com/settings/apps
      - PAT permissions - for organizational runners, use `admin:org`; for repo runners, use `repo`
   - Deploy the respective kubernetes secret manifest using your OAuth app or a base64 encoded version of your PAT
   - Run `make install-arc` then `make install-runner-set`
   - Verify the `arc-gha-rs-controller-xxxx` and `arc-runner-set-xxxxx-listener` pods came up
   - You're now ready to execute jobs in github using the `runs-on: <helm_deployment_name>` - in this case `arc-runner-set`

## Structure

The project is organized into three main directories:

- `helm`: Contains the Helm chart and related files for deploying the Actions Runner Controller(ARC).
- `images`: Includes Dockerfiles for building the images used in the ARC Runner Sets.
- `manifests`: Houses Kubernetes manifests for creating necessary infrastructure components.

### Helm

Inside the `helm` directory, you will find:

- `README.md`: Provides detailed instructions on how to use the Helm chart.
- `arc-controller-values.yaml`: Customizable values for the ARC deployment.
- `helm-base.yaml`, `helm-dind.yaml`, `helm-kaniko.yaml`: Various Helm configuration files for different deployment scenarios.
- `makefile`: A makefile with commands to help install, upgrade, and destroy the Helm chart deployments.

### Images

Within the `images` directory, there are:

- `base/dockerfile`: Dockerfile for building the base image used in the runner sets.
- `kaniko/dockerfile`: Dockerfile for building an ubuntu based image with kaniko go binaries injected into it.
  - The specific reason for this image is the kaniko image provided by kaniko comes with basic credential holders for ecr, acr, gar, etc. I wanted to be able to dynamically login to ecr using github actions marketplace actions and push the image there instead of having to statically define credentials. That way you can assume a role via OAuth, login to ECR, then push the kaniko image to that registry.
- `makefile`: A makefile with commands to build and push the Docker images.

### Manifests

The `manifests` folder includes Kubernetes manifests:

- `github-app.yaml`: Secret manifet for storing a GitHub OAuth application information.
- `github-pat.yaml`: Secret manifest for storing a GitHub personal access token.
- `pvc.yaml`: Persistent Volume Claim(pvc) for kubernetes mode runners
- `storage-class.yaml`: Defines the storage class used by pvc

## Getting Started

To deploy the GitHub actions-runner-controller and arc-runner-sets, follow these steps:

1. **Apply the Kubernetes Manifests**:
   - Apply the manifests in the `manifests` directory to your Kubernetes cluster to set up the necessary infrastructure components.
  
2. **Build the Docker Images**:
   - Review the `images` directory.
   - Determine if you need to use the Dockerfile in your own project with more customizations.

3. **Prepare the Helm Chart**:
   - Navigate to the `helm` directory.
   - Deploy the helm charts using the specific commands inside the makefile.

For detailed instructions on each step, please refer to the README.md files and makefiles in each directory.

## Contributing

Contributions are welcome! Please submit a pull request or open an issue if you have suggestions for improvement or have identified a bug.
