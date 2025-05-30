# CPS1 Key Concepts

CPS1 employs specific terminology to effectively model various system designs (architectures) and organizational team structures. To that end, we rely on two main concepts: **Templates** and **Workspaces**.

A **Template** contains the definition of how a development environment must be provisioned on your Kubernetes cluster, witch we call a **Workspace**.

The Template includes information such as source code repositories, ports, containers, services, programming languages and other resources needed to fully provision and run your entire application into a **Workspace**.

The **Workspace** has extra capabilities that augments developers productivity, such as an integrated web IDE and SSH access.

Let's dive into the details.

## Templates

A **Template** is the source of every ephemeral development environment in CPS1, that we call **Workspace**.

In CPS1, a **Template** is the definition of a provisioned **Workspace**.

Internally, a Template contains the configuration of the many parts of a running Workspace, that we call **Components**, and a container image that CPS1 builds and stores into an internal registry for fast **Workspace** provisioning.

Every Template has a base container image that is used as a starting point for CPS1 to add your configuration atop of it during the process of the Template build.

As a Platform Engineer, you can create a Template to define and configure what tools, languages and resources go into the final template image.

CPS1 will build a container image that will be used as a starting point for new Workspaces.

You don't need to manage Dockerfiles at this point and just provide an initial image.

### Components

A Template contains what we call **Components**.

A **Component** is the smallest functional unit that corresponds to a specific technology-related aspect of your application, such as the backend, frontend, or a database.

There are three types of Components: **Resources**, **Services**, and **Containers**.

#### Resources

A **Resource** refers to an external dependency that an application relies on to function, such as databases, caches, message brokers, and others.

<!-- TODO: dizer que pode ser uma dependencia --> 

CPS1 provides a list of commonly used Resource Components, including MongoDB, MySQL, PostgreSQL, Redis, RabbitMQ, and more, with support for multiple versions. This list is regularly updated and maintained.

Resource Components managed by CPS1 are deployed in isolation for development and are integral to each Workspace.

CPS1 can also manage external infrastructure necessary for development at runtime, such as services from public cloud vendors, integrating them into the Workspace lifecycle using Terraform.

#### Services

A **Service** runs code that typically exposes a network port. The code can be designed for a cloud-native environment, but this is not a requirement.

A **Service** has attributes that determine how it functions within the Workspace. These attributes are: **Code Repository**, **Packages**, and **Network Ports**.

The first attribute of a **Service** is to define a **Code Repository**.

<!-- TODO: dizer mais algo sobre como configurar e autenticação --> 

!!! note "Flexible repository structure support"
    
    CPS1 is agnostic about the structure of the repository. It supports repositories containing multiple distinct programming languages (commonly known as a monorepo) or a single programming language. For each language in the **Code Repository** of a **Service Component**, one or more **Packages** can be configured.

In CPS1, a **Package** refers to a combination of technologies that provide everything necessary to run, build, and test the code. It often includes a programming language, frameworks, libraries, runtime, and other tools.

**Packages** are self-contained units of installation code that run when a template container image is built and are designed to install on top of the Template base container image.

CPS1 provides a supported base image that is tested and compatible with the various Packages we provide out of the box, Examples include:

- Python
- Node.js
- .NET Core
- Java

Finally, each **Service** typically exposes one or more **Network Ports** (usually over TCP) that allow other services or external clients to communicate with it.

Ports can be internal or external. Internal ports allow services to interact with each other, while external ports enable end-users or clients to communicate with the service directly.

<!-- TODO: falar sobre a geraçao de portas automaticas q geral URLs --> 

!!! tip "Extending CPS1 for Platform Engineers"

    Missing the resource, tool or language that your organization uses? As a Platform Engineer, you can create and include your own **Packages** and **Resources** acording to your organization standards to CPS1.
    
    For details about supported languages, tools, and configurations, visit the CPS1 Contrib repository: [https://github.com/cps-1/helm-charts/tree/main/charts/cps1-contrib](https://github.com/cps-1/helm-charts/tree/main/charts/cps1-contrib).

## Workspaces

In CPS1, a **Workspace** is an ephemeral development environment created based on a given **Template**, with many additional capabilities compared to running locally on a developer’s laptop.

A Workspace operates entirely on your Kubernetes cluster where CPS1 is deployed. You don’t need to worry because CPS1 manages everything transparently, making Kubernetes operations invisible.

A Workspace includes everything defined in a Template, along with all programming languages and tools defined as **Packages** for each **Service** of the running application. There is no need to manually build base images.

Developers can access the **Workspace** using an integrated Visual Studio Code Web IDE directly from a web browser, eliminating the need for local software installation, or using an SSH connection.

When a developer accesses the **Workspace**, using the Visual Studio Code Web IDE or SSH, the source code of all configured **Services** will be checked out.

**Services** configured in the Template that expose a network port will be accessible via a URL automatically generated by CPS1.

The lifecycle of a Workspace begins when you create it and ends when you delete it. You can disconnect and reconnect to an active Workspace without affecting its running processes. Additionally, you can stop and restart a Workspace without losing any changes you have made.

## Summary of Key Concepts

- **Template**
    - Definition of how a development environment must be provisioned
    - Consists of multiple **Components**.

- **Component**
    - The smallest unit of an application, representing technology-related parts like backend, frontend, or database.
    - Two types: **Services** and **Resources**.

- **Service**:
    - Runs code, often exposing a network port.
    - Key attributes: **Code Repository**, **Packages**, and **Network Ports**.
    - Supports **monorepos** (multiple programing languages) and **single programing language** repositories.
    - **Packages**: Installs runtime and tools into the final template container image.
    - **Network Ports**: Allow internal and external communication.

- **Resource**
    - External dependencies like databases, caches, or message brokers.
    - CPS1 supports popular resources (e.g., MongoDB, PostgreSQL) and integrates cloud infrastructure via Terraform.
    - Resources are isolated for development within **Workspaces**.

- **Workspace**  
    - A cloud-based development environment managed on your Kubernetes cluster.
    - Offers enhanced capabilities compared to local development environments.
    - Accessible via a **Visual Studio Code Web IDE** through a browser.
    - Automatically checks out code on launch.
