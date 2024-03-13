# GitHub Arc Runner Controller

This project facilitates the creation and deployment of a GitHub Arc Runner Controller and Arc-Runner-Sets at the organizational or repository level. It includes a Helm chart with deployment commands to install in one's Kubernetes cluster, Docker images used inside the scale sets, and Kubernetes manifests to create the necessary components.

## Prerequisites

### Software:
- kubernetes/kubectl
- helm
- docker
- make
  
### Kubernetes infra:
- A kubernetes cluster
- Namespaces for the `arc-systems` and `arc-runners` - this can be customized to meet your needs (eg create a namespace per runner scale set in the helm installation)
  
## Structure

The project is organized into three main directories:

- `helm`: Contains the Helm chart and related files for deploying the Arc Runner Controller.
- `images`: Includes Dockerfiles for building the images used in the Arc Runner Sets.
- `manifests`: Houses Kubernetes manifests for creating necessary infrastructure components.

### Helm

Inside the `helm` directory, you will find:

- `README.md`: Provides detailed instructions on how to use the Helm chart.
- `arc-controller-values.yaml`: Customizable values for the Arc Runner Controller deployment.
- `helm-base.yaml`, `helm-dind.yaml`, `helm-kaniko.yaml`: Various Helm configuration files for different deployment scenarios.
- `makefile`: A makefile with commands to help install, upgrade, and destroy the Helm chart deployments.

### Images

Within the `images` directory, there are:

- `base/dockerfile`: Dockerfile for building the base image used in the runner sets.
- `kaniko/dockerfile`: Dockerfile for building an ubuntu based image with kaniko go binaries injected into it.
- `makefile`: A makefile with commands to build and push the Docker images.

### Manifests

The `manifests` folder includes Kubernetes manifests:

- `github-app.yaml`: Secret manifet for storing a GitHub OAuth application information.
- `github-pat.yaml`: Secret manifest for storing a GitHub personal access token.
- `pvc.yaml`: Persistent Volume Claim(pvc) for kubernetes mode runners
- `storage-class.yaml`: Defines the storage class used by pvc

## Getting Started

To deploy the GitHub Arc Runner Controller and Arc-Runner-Sets, follow these steps:

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
