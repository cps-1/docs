# What is Cloud Programming Shell (CPS1)?

**Cloud Programming Shell (CPS1) is a unified Platform Orchestrator and Cloud Development Environment solution.**

CPS1 bridges the gap between Platform Engineering and Developer Experience by unifying infrastructure provisioning and remote development into a single, self-service flow.

It's a self-hosted solution deployed on your Kubernetes cluster, enhancing development workflows with an intuitive orchestration engine that automates the provisioning of development environments.

## What is Platform Engineering?

While Platform Engineering is an expansive field without a single industry-standard definition, its core principles are best understood through the perspectives of the experts and organizations shaping the discipline today.

What is Platform Engineering according to CNCF:

> The main goal of Platform Engineering is to improve the developer experience (DevEx) and optimize software delivery.
>
> **Natália Granato**, CNCF Ambassador, [What is platform engineering?](https://www.cncf.io/blog/2025/11/19/what-is-platform-engineering/)

Acording to Google Cloud:

> Platform Engineering is the practice of building useful abstractions and self-service infrastructure within an organization, to unify scattered tools and accelerate developer productivity.
>
> **Darren Evans**, **Megan O'Keefe**, Google Cloud, [Light the way ahead: Platform Engineering, Golden Paths, and the power of self-service](https://cloud.google.com/blog/products/application-development/golden-paths-for-engineering-execution-consistency)

Acording to the author of the book [Team Topologies](https://teamtopologies.com):

> The ultimate goal of Platform Engineering is to accelerate the flow of value to the customer by reducing cognitive load in the system at the optimal level of investment.
>
> **Manuel Pais**, Team Topologies, [Team Topologies Platform Engineering](https://teamtopologies.com/platform-engineering)

While definitions vary, the consensus is clear: Platform Engineering is about shifting the complexity 'down' into a self-service product so developers can focus on business value.

The platform's job is to take the pain so the developer doesn't have to.

### What is a Platform Orchestrator?

For many years, the industry embraced the “You Build It, You Run It” principle, popularized by Amazon CTO Werner Vogels. This model placed responsibility for infrastructure, security, and networking directly on developers.

As cloud-native ecosystems grew in scale and complexity, this approach became unsustainable, imposing excessive cognitive load on development teams.

Platform Engineering emerged to deliberately shift these responsibilities downward. Within this context, the Platform Orchestrator provides a developer-centric mechanism for on-demand infrastructure provisioning, governed by standardized organizational policies.

The Platform Orchestrator bridges high-level application requirements with underlying infrastructure by managing networking, storage, identity, and secrets. By automating resource integration and configuration, it enables developers to focus on delivering business logic rather than operating infrastructure.

Functioning as the platform’s control plane, the Platform Orchestrator manages the full lifecycle of environments and may abstract or replace traditional tooling such as Terraform and Ansible from the developer’s perspective.

At its core, a Platform Orchestrator delivers self-service engine for infrastructure delivery.

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

* Metadata decay: Information created in one tool (e.g., a database connection string in Terraform) becomes "stale" or lost by the time it reaches the second tool (the IDE).
* The "N+1" configuration problem: If you change a port in your infra orchestrator, you now have an "N+1" task: you must manually find and update every dependent environment. If you have 50 developers, that’s 50 potential points of failure.
* Fragile pipelines: Glue code is rarely unit-tested. When the Orchestrator updates its API, the "glue" breaks, and suddenly no one can code.

## Platform Orchestrator vs. Cloud Development Environment

When you glue a Platform Orchestrator to a Cloud Development Environment, you encounter the "Cross-Configuration Gap."

* **The Scenario**: Your Orchestrator provisions a dynamic PostgreSQL instance for a developer's feature branch.
* **The Problem**: The Orchestrator assign a dynamic internal DNS name.
* **The Manual Bridge**: The developer now has to manually copy-paste that connection string into their `.env` file or their VS Code settings inside the CDE (or even locally).

Another common scenario, because the tools are separate, developers often hard-code secrets or use "test1234" just to bypass the friction of the integration.

In this model, the self-service dream dies because the developer is still stuck "configuring" instead of "coding."

## Why CPS1 was created

Given the inherent complexity of modern systems, we believe that development must shift from local workstations to automated, managed cloud infrastructure. This transition ensures that the development environment scales alongside the system it supports.

Furthermore, to eliminate the "glue" problem, the environment in which application code is written, including all external dependencies, must be treated as a single, cohesive unit. These elements are fundamentally interdependent; one cannot function effectively without the other.

This shift is essential for enhancing software development and delivery velocity. It allows us to maintain high standards of quality and consistency without necessitating an increase in headcount.

To realize this vision, we must move away from fragmented local setups and adopt a new paradigm. By unifying development environments with their required infrastructure under a single configuration and workflow, we create a more resilient and efficient path forward.


