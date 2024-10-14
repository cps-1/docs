We believe that achieving scalability in software delivery requires a centralized approach to managing development environments, moving away from individual work on each developer's laptop.

To understand our vision for CPS1, we must understand the concepts of inner and outer development loops. For those unfamiliar with the terminology, these two phrases refer to different aspects of software development workflow.

CPS1 is used at the code development stage of the workflow, empowering your developers and not interfering with your current CI/CD pipelines. We improve the work done by developers until the code is pushed to source control. That is commonly called inner development loop.

The inner loop involves an individual developer's cycle of coding, building, and testing changes, allowing for rapid feedback until the code is ready for review as a pull request (PR). This process occurs on CPS1 instead of the developer's computer within a local environment,

When considering where development happens, each developer accesses a Web IDE that is the entry door for the Workspace. Each Workspace is where the developer code, builds and tests a given application, which we call just App. The developers finally commits and pushes code to Source Control, usually triggering CI/CD pipelines.

![Screenshot](assets/cps1-overview.png)

In contrast, the outer loop takes place after a developer pushes code to a repository. This phase involves merging changes into the main source, usually triggering a CI/CD pipeline that tests and builds the new code, ultimately creating a production-ready artifact for deployment.

What advantages does CPS1 bring:
Easily offers a production-like environment with all infrastructure, IDEs, and tools your developers need.
Launch your entire application with a specific version of your code, to allow for end-to-end testing, including all services and resource dependencies.
Code any part of your application directly on the cloud and see the effects in real-time, significantly reducing iteration time.
Liberate developers and platform teams from dealing with provisioning of environments and resource dependencies.
Goodbye to the complexities of setting up local environments and the discrepancies between development and production.