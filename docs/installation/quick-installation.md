# Quick Installation

For proof-of-concept scenarios, we provide an installation script that installs CPS1 locally, without requiring a Kubernetes cluster.

## Prerequisites
Ensure the following tools are installed on your system:

- [Docker](https://docs.docker.com/get-docker/)
- [Kind](https://kind.sigs.k8s.io/docs/user/quick-start/)
- [Helm](https://helm.sh/docs/intro/install/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)

## Running the installer

```
curl https://helm.cps1.tech/cps1-installer.sh | bash
```

After the installation finishes, you can access CPS1 at [http://cps1.localhost:3001](http://cps1.localhost:3001).

For a production grade installation, follow the [Production Installation](/installing/production-intallation.md) guide.

## Logging into your CPS1 instance

When a fresh installation is done, there are no users created.

Once you access CPS1 for the first time, it will prompted you to create an `Admin` user account.

Provide a username and password and you are ready to create your first Workspace!

If you encounter any issues or have feedback, please open an issue in our repository: [https://github.com/cps-1/cps1](https://github.com/cps-1/cps1)