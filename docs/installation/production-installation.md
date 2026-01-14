# Production Setup

CPS1 is installed on a Kubernetes cluster to transparently handle all necessary operations that support our core features.

!!! warning Dedicated Kubernetes cluster for CPS1

    We strongly recommend that CPS1 must be deployed on a Kubernetes cluster dedicated for development and doesn't have any production workloads.


We support all major managed Kubernetes vendors, including Amazon EKS, Azure AKS, Google GKE, and Oracle EKS.

## Requirements

### Kubernetes Requirements

CPS1 works out of the box on any Kubernetes vendor or provider, as it does not use any vendor-specific features.

We support all currently supported Kubernetes versions by the major cloud providers, requiring a minimum of Kubernetes version 1.30 or newer.

You must also have CertManager (version 1.12 or newer) and Nginx Ingress Controller (version 1.9.0 or newer) deployed on the cluster.

- [CertManager Installation Guide](https://cert-manager.io/docs/installation/)
- [NGINX Ingress Controller Installation Guide](https://kubernetes.github.io/ingress-nginx/deploy/)

### DNS Requirements

CPS1 requires two DNS records:

- An DNS record for `cps1.example.com`, pointing to the Ingress controller's external IP address, used by the Ingress
- A wildcard DNS record for `*.cps1.example.com`, pointing to the external IP address of your cluster's LoadBalancer service.

The availability of IP addresses for the Ingress and LoadBalancer depends on how your cluster is provisioned and managed.

### Storage Requirements

For stringer isolation and disk space usage, CPS1 uses one PVC per user.

Make sure that the default storageClass your cluster provides read-write-many.

## Installing with Helm charts

The supported installation method is using the [official CPS1 Helm Charts repository](https://github.com/cps-1/helm-charts/).

CertManager and Nginx Ingress Controller must be installed and configured separately, as they are not included in the provided Helm charts.

### Add CPS1 chart repository

```
helm repo add cps1 https://helm.cps1.tech
helm repo update
```

### Install CPS1 Custom Resouce Definitions

CRDs must be installed first. This step is required and does not support custom values.
```
helm install --namespace cps1 --create-namespace cps1-crds cps1/cps1-crds
```

### Install CPS1 Platform

The following Helm values are required for the platform installation:

- `config.hostname`: The fully qualified domain name for your deployment
- `config.tls.clusterIssuer`: A valid ClusterIssuer configured in CertManager to issue TLS certificates

Minimal install command:
```
helm install -n cps1 cps1-platform cps1/cps1-platform \
  --set config.hostname=<your_domain> \
  --set config.tls.clusterIssuer=<your_cluster_issuer>
```

To review all configurable options, including GitHub and GitLab integration, run:
```
helm show values cps1/cps1-platform
```

!!! note CPS1 Community Edition

    CPS1 Community Edition is free to use within your organization, with a limit of 5 active users and one Kubernetes cluster.

    For teams with more than 5 users or requiring multiple clusters, please [upgrade to the Enterprise Edition](https://www.cps1.tech/talk-to-sales).

    By installing CPS1 Community Edition, you accept the [End User License Agreement (EULA)](https://www.cps1.tech/eula).

### Install packages, resources and templates

CPS1 Contrib is a curated collection of packages, resources, and templates that extend the capabilities of the CPS1 platform.

For details about supported languages, tools, and configurations, visit the CPS1 Contrib repository: [https://github.com/cps-1/helm-charts/tree/main/charts/cps1-contrib](https://github.com/cps-1/helm-charts/tree/main/charts/cps1-contrib).

The command below installs all packages and resources, and includes only the development environment templates for NodeJS and Python.

```
helm install -n cps1 cps1-contrib cps1/cps1-contrib \
  --set 'includeTemplates={nodejs,python}'
```

To include additional templates, add them to the `includeTemplates` list (e.g., `'includeTemplates={nodejs,python,go}'`).

You can find the full list of available templates in the [CPS1 Contrib repository](https://github.com/cps-1/helm-charts/tree/main/charts/cps1-contrib/).

!!! tip Contribute 
    We welcome contributios of additional packages, resources, and templates to CPS1 Contrib! Please see our [Contribution Guidelines](https://github.com/cps-1/helm-charts/blob/main/charts/cps1-contrib/CONTRIBUTING.md) for details on how to get started. Feedback and requests are also welcome!

### Logging into your CPS1 instance

When a fresh installation is done, there are no users created.

Once you access CPS1 for the first time, it will prompted you to create an `Admin` user account.

Provide a username and password and you are ready to create your first Workspace!

If you encounter any issues or have feedback, please open an issue in our repository: [https://github.com/cps-1/cps1](https://github.com/cps-1/cps1)
