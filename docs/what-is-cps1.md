# What is Cloud Programming Shell (CPS1)?

Cloud Programming Shell (CPS1) is a unified Platform Orchestrator and Cloud Development Environment solution.

CPS1 bridges the gap between Platform Engineering and Developer Experience by unifying infrastructure provisioning and remote development into a single, self-service flow.

Cloud Programming Shell (CPS1) is a self-hosted solution deployed on your Kubernetes cluster, enhancing development workflows with an intuitive templating engine that automates the provisioning of ephemeral development environments.

Platform engineers can easily customize and extend CPS1, eliminate manual setup, and enforce consistency in ephemeral environments, while offering developers self-service and the flexibility they need.

## What is Platform Engineering?

TODO
Team topologies, time de plataforma,

Falar de disciplinas como env mgmt e 

### What is a Platform Orchestrator?

TODO, Terraform ou GitOps tools, massdriver, etc

### What is a Cloud Development Environment?

A Cloud Development Environment (CDE) consists of pre-configured software development tools that are accessible in the cloud and on demand. It includes all the necessary dependencies, allowing developers to start coding within moments, without the need for local installation and configuration on their computers.

This paradigm offers several advantages, such as:

- Standardized and centrally managed environments: Development environments are always stable and ready for coding.
- Access to powerful cloud resources: Leverage powerful cloud machines without being limited by local CPU and memory constraints.
- Automatic updates and security patches: Library and toolchain updates are always current, eliminating the need for local maintenance.
- Portability: Code from anywhere, at any time, with a consistent environment that matches production.
- Enhanced collaboration: Facilitates easy remote collaboration and troubleshooting.

Fundamentally, Cloud Development Environments (CDEs) shift the paradigm from local coding on laptops to remote development.

To learn more about CDEs and the advantages of this paradigm shift, here are four recommended articles for a deeper understanding of the subject:

| Article     | Description                          | Author |
| ----------- | ------------------------------------ | ------ |
| [What Is a Cloud Development Environment?](https://www.dreamhost.com/blog/cloud-development-environment/) | This article explains the concept of Cloud Development Environments (CDEs), detailing how they provide developers with accessible, pre-configured tools in the cloud. It highlights the benefits of using CDEs, such as improved collaboration, reduced setup time, and enhanced scalability for development teams. | Matt Stamp |
| [Cloud Development Environments](https://newsletter.pragmaticengineer.com/p/cloud-development-environments) | In this newsletter, the author discusses the rise of Cloud Development Environments, emphasizing their role in streamlining software development processes. It covers the advantages of CDEs over traditional local setups, including flexibility and efficiency, and shares insights on adopting this paradigm in development workflows. | Gergely Orosz |

## The General Problem of "Glue" in Platform Engineering

In software, "glue" is the custom code, scripts, and manual handoffs used to make different tools talk to each other. In Platform Engineering, glueing results in three major pains:

* Metadata Decay: Information created in one tool (e.g., a database connection string in Terraform) becomes "stale" or lost by the time it reaches the second tool (the IDE).
* The "N+1" Configuration Problem: If you change a port in your infra orchestrator, you now have an "N+1" task: you must manually find and update every dependent environment. If you have 50 developers, that’s 50 potential points of failure.
* Fragile Pipelines: Glue code is rarely unit-tested. When the Orchestrator updates its API, the "glue" breaks, and suddenly no one can code.

## Platform Orchestrator vs. Cloud Development Environment

When you glue a Platform Orchestrator to a CDE, you encounter the "Cross-Configuration Gap."

The Scenario: Your Orchestrator provisions a dynamic PostgreSQL instance for a developer's feature branch.

The Problem: The Orchestrator might assign a random port (e.g., 5432 → 32145) or a dynamic internal DNS name.

The Manual Bridge: The developer now has to manually copy-paste that connection string into their `.env` file or their VS Code settings inside the CDE (or even locally).

Security Leaks: Because the tools are separate, developers often hard-code secrets or use "test1234" just to bypass the friction of the integration.

In this model, the "Self-Service" dream dies because the developer is still stuck "configuring" instead of "coding."

## Why CPS1 was created

We believe that, given the complexity and other characteristics of modern systems, development must take place on a managed cloud infrastructure with automation, rather than locally on each contributor's laptop.

This change is essential to increasing software development and delivery capabilities by 10x while maintaining quality and consistency, all without increasing the number of people involved.

To achieve the results of our vision, we believe changing the paradigm and moving away from local development environments is the best path forward.

It is also crucial to make the transition seamless from laptop-based local environments to the cloud by utilizing automation, eliminating the need for labor-intensive manual updates of software projects.

