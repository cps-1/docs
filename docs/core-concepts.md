# CPS1 Core Concepts

CPS1 employs specific terminology to effectively model various system designs (architectures) and organizational team structures.

The first concept that we need to understand is the **App** definition.

## The App definition

In CPS1, an **App** refers to a system that carries out a specific business function within your organization, such as payroll or payment processing. The term workload is also commonly used in cloud-native contexts and has a similar meaning to **App**.

This concept allows us to abstract implementation details and concentrate on the functionality delivered to end users within your organization.

An App typically provides a user interface or a public API and is composed of one or more **Components**.

## The Component definition

In CPS1, a **Component** represents the individual parts of an App. 

A **Component** is the smallest functional unit that corresponds to a specific technology-related aspect of an App, such as the backend, frontend, or a database.

There are two types of Components: **Service Components** and **Resource Components**.

### Service Components

A **Service Component** runs code that typically exposes a network port. The code can be designed for a cloud-native environment, but this is not a requirement.

A **Service Component** has attributes that determine how it functions within an App. The attributes are: **Code Repository**, **Stacks**, **Tasks** and **Network Ports**.

The first and obligatory attribute of a **Service Component** is to define a **Code Repository**.

!!! note "Flexible repository structure support"
    
    CPS1 is agnostic about the structure of the repository. It supports repositories containing multiple distinct programming languages (commonly known as a monorepo) or a single programming language. For each language in the **Code Repository** of a **Service Component**, one or more **Stacks** must be configured.

In software development, a stack typically refers to a combination of technologies used together to build software. It often includes a programming language, frameworks, libraries, runtime and other tools.

In CPS1, **Stacks** provide the runtime and other utilities necessary to run, build and test the code. Examples:

- Python 3
- Node.js 22
- .NET Core 8

**Tasks** are commands that perform common operations used by developers to manage and build their projects, often automated through scripts or build tools. Examples of **Tasks** used by a **Service Component** include building and running code, executing unit tests, linting, and code formatting.

Finally, each **Service Component** typically exposes one or more **Network Ports** (usually over TCP) that allows other services or external clients to communicate with it.

Ports can be internal or external. Internal ports allow services to interact with each other, while external ports enable end-users or clients to communicate with the service directly.

### Resource Components

A **Resource Component** refers to an external dependency that an App relies on to function, such as databases, caches, message brokers, and others.

CPS1 provides a list of commonly used Resource Components, including MongoDB, MySQL, PostgreSQL, Redis, RabbitMQ, and more, with support for multiple versions. This list is regularly updated and maintained.

Resource Components managed by CPS1 are deployed in isolation for development and are integral to each workspace.

CPS1 can also manage external infrastructure necessary for development at runtime, such as services from public cloud vendors, integrating them into the workspace lifecycle using Terraform.

!!! tip "Automated New Components with CPS1"

    Modern Apps are large and complex, with dozens of services, repositories, and dependencies. Manually configuring each Component in such cases can be tedious and error-prone.
    
    CPS1 uses detection technology to quickly scan multiple source code repositories and accurately identify Stacks, Tasks, Network Ports of Service Components, and Resource Components — such as databases and message brokers — without requiring manual configuration.

## The Workspace definition

In CPS1, a **Workspace** is a development environment that runs an App but offers additional capabilities compared to running the App locally on a developer’s laptop.

A Workspace operates entirely on your Kubernetes cluster where CPS1 is deployed. You don’t need to worry because CPS1 manages everything transparently, making Kubernetes operations invisible.

A Workspace development environment includes basic Linux commands, along with all programming languages and tools defined as **Stacks** for each **Component Service** of the running App. There is no need to manually build base images.

Developers can access the **Workspace** using a integrated Visual Studio Code Web IDE directly from a web browser, eliminating the need for local software installation.

When a developer accesses the Visual Studio Code Web IDE, the source code of all Services will be checked out. If a Build Task and Run Task are defined, those services will be running automatically.

When the developer access the Visual Studio Code Web IDE, the source code of all **Service Components** will be checked out. Also, **Service Components** that have a **Run Task** defined will be running.

**Service Components** configured to expose a network port will be accessible via a URL automatically generated by CPS1.

The lifecycle of a Workspace begins when you create it and ends when you delete it. You can disconnect and reconnect to an active Workspace without affecting its running processes. Additionally, you can stop and restart a Workspace without losing any changes you have made.

## The Project definition

A **Project** groups a collection of Apps and allows you to manage collaborators and permissions.

Projects can mirror your organization’s team structure and how each team develops an App, tracking metrics related to infrastructure usage and cost management. 

Due to the complexity of modern Apps, the boundaries between which **Service Components** and **Resource Components** belong to an App or Project vary on a case-by-case basis, depending on each organization’s specific needs — especially regarding code and ownership.

## Summary of Core Concepts

- **App**
    - A system that performs a specific business function (e.g., payroll, payment processing).
    - Provides either a user interface or a public API.
    - Consists of multiple **Components**.

- **Component**
    - The smallest unit of an App, representing technology-related parts like backend, frontend, or database.
    - Two types: **Service Components** and **Resource Components**.

- **Service Component**:
    - Runs code, often exposing a network port.
    - Key attributes: **Code Repository**, **Stacks**, **Tasks**, and **Network Ports**.
    - Supports **monorepos** (multiple programing languages) and **single programing language** repositories.
    - **Stacks**: Define runtime and tools (e.g., Python, Node.js).
    - **Tasks**: Commands used to build, run, or test code.
    - **Network Ports**: Allow internal and external communication.

- **Resource Component**
    - External dependencies like databases, caches, or message brokers.
    - CPS1 supports popular services (e.g., MongoDB, PostgreSQL) and integrates cloud infrastructure via Terraform.
    - Resource Components are isolated for development within **Workspaces**.

- **Workspace**  
    - A cloud-based development environment managed on your Kubernetes cluster.
    - Offers enhanced capabilities compared to local development environments.
    - Accessible via a **Visual Studio Code Web IDE** through a browser.
    - Automatically checks out and runs code on launch.

- **Projects**
    - Group multiple Apps to manage permissions and collaborators.
    - Mirror the organization’s team structure and track infrastructure usage and costs.
    - Define ownership and component boundaries based on organizational needs.
