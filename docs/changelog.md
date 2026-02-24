# Changelog

## 0.5.1 <small>February 9, 2026</small> { id="0.5.1" }

- Fixed the generated SSH hostname to connect through the SSH gateway. 0.5.0
introduced a regression that could generate SSH hostnames that were not a legal
IDNA2008 name (larger than 63 characters).

## 0.5.0 <small>January 23, 2026</small> { id="0.5.0" }

- Fixed the usage of multiple environment variables through the SSH gateway
- Improved how the SSH gateway sets environment variables in interactive shells
- Updated SSH and HTTP gateway to listen both to IPv4 and IPv6 requests
- Validate duplicate IDs for workspaces and resources in templates definitions
- Normalize and mangle Kubernetes object names created by the CPS1 Operator.
Most of the created objects now contains a random suffix (similar to
Kubernetes' vanilla objects such as Pods) to avoid name collisions. Normalized
names uses the beginning and ending of the original name, respecting the
created object name length limit. Before this change there was a small chance
of generating invalid Kubernetes objects names.
- Introduced multiple volume strategies for environments workspaces'. The
`sharedPerUser` strategy uses a single PVC of the user namespace across their
environments. While the `isolatedPerWorkspace` strategy uses one PVC per
created workspace. Those options are configured by the `workspaceVolumes`
option, and also supports defining the used `StorageClass` and `accessMode`.
- Added the option to select a custom branch for each repository of each
workspace when creating a new environment.
- Fixed an error when a resource type is changed in the template form. The form
didn't properly reset with the default values of the newly selected resource.
- Fixed CEL statements output in resources. They were always incorrectly
coerced into strings, now they respect the source input type.
- Added a retry option to recreate workspaces
- Added an option to visualize setup errors for workspaces
- Fixed some errors that could occur between the CPS1 operator and the Kubernetes
API when it didn't properly finished a TLS connection (sending a close_notify
message). The error would occur when the operator attempt to reuse a connection
from a connection pool and that connection was ended by the server side. The
fix relaxes the TLS settings to tolerate Kubernetes API servers that doesn't
implement Closure Alerts as per RFC 5246 section 7.2.1.

## 0.4.1 <small>December 16, 2025</small> { id="0.4.1" }

- Version 0.3 added a change where every template is built with [user namespaces](https://kubernetes.io/docs/concepts/workloads/pods/user-namespaces/) for Kubernetes 1.33 or newer. But some Kubernetes distributions/worker nodes combinations still doesn't properly support this feature such as Kind (Kubernetes in Docker) and EKS clusters with Bottlerocket. Therefore, now this behavior is opt-in. You can enable it setting CPS1's config `buildWithUserNamespaces` to `true` (it is `false` by default).
- Fixed an issue where an SSH channel would be closed before completely streaming an exec's stderr if the stdout finished streaming.

## 0.4.0 <small>December 11, 2025</small> { id="0.4.0" }

- IDs from resources and workspaces are translated depending on the context to be used in Kubernetes objects name and CEL statements.
- More variables are available in CEL contexts to refer to services exposed by other workspaces. Now it's easy to connect multiple microservices within a single environment:
- The SSH gateway was updated to support JetBrains Gateway.
- Fixed a bug that could make a new environment page become empty
- Fixed the build logs display for templates with multiple workspaces

## 0.3.1 <small>December 02, 2025</small> { id="0.3.1" }

- Add validations in UI and CRDs to block invalid Resources and Workspaces IDs

## 0.3.0 <small>December 02, 2025</small> { id="0.3.0" }

- Add graceful shutdown to the SSH gateway
- Fix a security vulnerability where a custom built malicious SSH client could crash the SSH gateway
- Improve the web UI performance by removing some redundant network requests
- Add support for Kubernetes 1.34
- Fix progress display when a Workspace is starting
- Make the pause/resume button more responsive
- Fix the workspace list showing deleted workspaces
- Improve package selection UI in the template form
- Fix the HTTP gateway blocking preflight requests
- Fix the template form losing data when deleting a package
- Sort template options by name when starting a worskpace
- Build images isolated in user namespaces when possible (kubernetes 1.33 or newer and Linux kernel 6.3 or newer)
- Harden some security settings for workspace pods
- Add ResourceSets, Workspaces and Environments CRDs
- Add TemplateSnapshot and EnvironmentSnapshot
- Resolve CEL statements in ResourceSets
- Update UI to reflect new concepts: an Environment is created from a Template. Templates/Environments contains multiple Workspaces and Resources.
- Disable SSH and WebIDE buttons while workspace is not ready
- Remove some noise from CPS1 server logs
- Improve operator performance removing some network requests to the Kubernetes API
- Add default annotations for user namespaces' Service Accounts
- Resolve CEL statements in Workspaces' environment variables

## 0.2.0 <small>August 08, 2025</small> { id="0.2.0" }

- Fix gateway closing SSH connections after some minutes
- Improve gateway performance for SSH connections
- Improve gateway performance for HTTP requests
- Slightly decrease gateway memory usage
- Make users SSH into their $HOME instead of `/`
- Make the gateway consumes less resources from the Kubernetes API Server
- Add support for tag properties in packages
- Fix a bug where resources and services forms would show default values instead of persisted values
- Add support for custom icons in packages
- Add the `apt` package to the contrib chart
- Add the `kubectl` package to the contrib chart

## 0.1.0 <small>July 16, 2025</small> { id="0.1.0" }

- Initial release
