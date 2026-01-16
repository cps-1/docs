# Key Concepts

CPS1 employs specific terminology to effectively model various workloads and organizational team structures. Our framework is built on four core concepts: **Workspaces**, **Resources**, **Templates**, and **Environments**.

## Building Blocks: Workspaces and Resources

Developers connect their preferred IDE to a **Workspace** to write, run, debug, and test code, shifting active development off their local machine, ensuring environment parity. Each Workspace comes with all required tools pre-installed, requiring zero setup, and allows for sharing the live state of running code for immediate feedback.

Code rarely runs in isolation. It relies on external dependencies, such as databases, caches, and message brokers, to function correctly. We define these dependencies as **Resources**.

### Workspaces

A **Workspace** serves as a reproducible environment designed specifically for application development. It contains the source code, network ports, programming languages, and various tools required to build and run your software. 

Organizations can standardize development setups and tooling across entire teams using Workspaces. This consistency eliminates the "it works on my machine" problem inherent in traditional local development.

Furthermore, because Workspaces runs on a Kubernetes cluster, they offer significantly greater compute capacity compared to a standard laptop.

The Workspace is accessible using SSH. Most modern IDEs support remote development through this protocol, delivering a seamless Developer Experience by allowing you to work in a remote environment as if it were local.

Common IDEs for remote development include:

* [VS Code Remote Development](https://code.visualstudio.com/docs/remote/remote-overview)
* [IntelliJ IDEA Remote development overview](https://www.jetbrains.com/help/idea/remote-development-overview.html)
* [Zed Remote Development](https://zed.dev/docs/remote-development)

Consider each Workspaces as a functional unit that corresponds to a specific technical component of your application, such as the frontend or the backend.

A Workspace has attributes that determine how it functions. These attributes are: **Code Repositories**, **Packages**, **Network Ports**, and **Environment Variables**.

#### Packages

Every Workspace utilizes a container **Base Image** and a set of **Packages**.

These Packages are integrated during the Workspace build process. They function as self-contained units of installation that typically includes programming languages, frameworks, libraries, and relevant tools necessary to build, run and test your application code.

The primary advantage of this system is that Platform Engineers can define and provide all necessary tools and languages without manually writing or maintaining Dockerfiles.

CPS1 handles the underlying container image build, ensuring that the resulting Workspace image is consistent, optimized, and ready for immediate development.

!!! tip "Packages in the CPS1 Catalog"

    CPS1 provides a wide variety of tested, out-of-the-box Packages for popular stacks such as Python, Node.js,
    .NET Core, and Java. You can explore these options in the CPS1 Catalog.
    
    For details about supported languages, tools, and configurations, visit the CPS1 Catalog repository: [https://github.com/cps-1/helm-charts/tree/main/charts/cps1-catalog](https://github.com/cps-1/helm-charts/tree/main/charts/cps1-catalog).

#### Code Repositories

To further enhance the Developer Experience, a Workspace can be configured with a specific set of Git repositories. These repositories are automatically cloned during the Workspace provisioning process, ensuring the code is ready for development immediately upon startup.

CPS1 remains agnostic regarding the structure of each repository. The platform fully supports diverse architectures, including monorepos containing multiple distinct programming languages as well as standard repositories focused on a single language.

For for more details refer to the [Git Repository Integration](git-repository-integration.md) guide.

#### Network Ports

Applications typically expose one or more **Network Ports**, usually over TCP, to enable communication with other services or external clients.

CPS1 allows you to configure and expose these Network Ports for applications running within a Workspace. Each configured port is automatically mapped to a unique, secure URL.

These preview URLs empower team members to share their progress and gather feedback instantly, bypassing the need for slow CI/CD pipelines. For enhanced security, access to these URLs is restricted exclusively to authenticated users within your CPS1 instance.

#### Environment Variables

The most common method for configuring an application is through the use of **Environment Variables**. These variables are essential for externalizing configuration, which allows applications to adapt without requiring code changes. This practice makes the codebase more portable, maintainable, and secure by strictly separating sensitive settings from the source code.

Environment Variables are typically utilized for managing database connection strings, feature flags, and system directories.

A Workspace can be pre-configured with a specific set of Environment Variables that are immediately accessible upon startup.

By automating this setup, CPS1 eliminates the need for developers to perform manual configuration, allowing them to remain focused on writing code.

### Resources

A **Resource** refers to an external dependency that an application requires to function, such as a database, cache, or message broker. Resources represent the essential infrastructure components necessary for an application to operate correctly.

One of the primary challenges in Platform Engineering is the automated provisioning and maintenance of developer infrastructure. Managing the lifecycle of these components is critical, particularly the decommissioning of unused resources to prevent unnecessary cloud costs.

Technically, a Resource in CPS1 consists of a predefined set of instructions that dictate how a specific infrastructure component should be created and managed.

CPS1 utilizes an internal orchestrator to provision Resources according to these instructions. The orchestrator maintains the state of these components throughout their lifecycle. A Resource can be provisioned internally on the Kubernetes cluster where CPS1 resides, or it can manage external infrastructure from public cloud providers at runtime.

By integrating these external services into the Environment lifecycle, CPS1 ensures that all necessary infrastructure is automatically provisioned when needed and cleaned up when no longer in use.

!!! tip "Resources in the CPS1 Catalog"

    CPS1 provides a list of commonly used Resources, including MariaDB, MySQL, PostgreSQL, Redis, AWS SNS, AWS RDS, with support for multiple versions. You can explore these options in the CPS1 Catalog.
    
    For details, visit the CPS1 Catalog repository: [https://github.com/cps-1/helm-charts/tree/main/charts/cps1-catalog](https://github.com/cps-1/helm-charts/tree/main/charts/cps1-catalog).

## The Lifecycle: Templates and Environments

A **Template** serves as the authoritative blueprint for creating **Environments**. It contains the precise definition of how a development environment must be provisioned, acting as the static specification for what eventually becomes a live, running instance.

The uniqueness of CPS1 lies in its ability to unify all development requirements into a single workflow. By combining Workspaces and Resources within a single definition, the platform ensures that the entire application stack is reproducible and consistent.

### Templates

A **Template** is the configuration that dictates how CPS1 provisions an **Environment**.

It acts as a manifest that declares which Workspaces (the code and tools) and which Resources (the infrastructure and dependencies) are required.

This approach allows Platform Engineers to create standandarzied development environments, ensuring that every developer starts with an identical, optimized setup.

### Environments

In CPS1, an **Environment** is an ephemeral instance created from a specific Template. These environments provide capabilities that far exceed the limitations of a local laptop.

Multiple Environments can be created simultaneously from a single Template. This capability allows developers on the same team to work on different features of the same application in complete isolation. By utilizing independent environments, team members can develop, test, and experiment without the risk of interfering with one another's progress or stability.

During the Environment provisioning process, CPS1 manages all underlying orchestration transparently. Resources can be provisioned internally within the Kubernetes cluster where CPS1 resides or externally through public cloud providers.

Every Workspace within an Environment is provisioned directly on the Kubernetes cluster hosting the CPS1 platform. A significant advantage of this architecture is that CPS1 handles complex Kubernetes operations in a way that remains completely invisible to the end user. This abstraction allows Platform Engineers to leverage the power of container orchestration without needing to manage its technical intricacies.

An Environment lifecycle begins upon creation and concludes when it is deleted, invluding all associated Resources. This model supports modern development workflows in several ways:

* Persistent sessions: You can disconnect and reconnect to an active Workspace without interrupting running processes.
* State preservation: You can stop and restart Workspaces without losing any configuration changes or files.
* On-Demand scalability: Environments utilize the compute power of the cluster rather than local hardware.

## Summary of Key Concepts

- **Workspace**
    - The smallest unit of an application, representing technology-related parts like backend or frontend.
    - Runs code, often exposing a network port.
    - Key attributes: **Code Repository**, **Packages**, **Network Ports** and **Environment Variables**.
    - Supports **monorepos** (multiple programing languages) and **single programing language** repositories.
    - **Packages**: Installs runtime and tools into the final Workspace container image.
    - **Network Ports**: Allow communication with running code inside the Workspace.
    - **Code Repository**: Automatically checks out code on Workspace launch.
    - **Environment Variables**: Defines configuration and behavior of the application.

- **Resource**
    - External dependencies like databases, caches, or message brokers.
    - Contains definitions that dictate how a specific infrastructure component should be created and managed.

- **Template**
    - Definition of how a development environment must be provisioned.
    - Consists of **Workspaces** and **Resources**.

- **Environment**  
    - A cloud-based development environment managed on your Kubernetes cluster.
    - Offers enhanced capabilities compared to local development environments.
    - Provisioned Workspaces and Resources
