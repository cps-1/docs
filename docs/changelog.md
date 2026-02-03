# Changelog

## 0.5.0 <small>January 23, 2026</small> { id="0.5.0" }

- Added the option to specify a git branch instead of the default one for each repository in each workspace.
- Added options to retry provisioning a workspace and visualizing setup error logs.
- Most Kubernetes objects created by CPS1 now have their names normalized. That is, their name is summarized to fit their type name length restriction and a random suffix is added to avoid collisions. This prevent some errors that could happen while provisioning environments with very large names that created resources with a very strict name size (e.g statefulsets).

- Added a new configuration option to set which strategy to use for volume allocation for workspaces:
    - `sharedPerUser`: every workspace created by that user will consume a single volume from their namespace
    - `isolatedPerWorkspace`: every workspace gets its own isolated volume

The default strategy is `isolatedPerWorkspace`. To change it, configure the `workspaceVolumes` in the config object:
```yaml
workspaceVolumes:
  allocationStrategy: isolatedPerWorkspace  # Or "sharedPerUser"
```

Other options added to `workspaceVolumes` includes `size`, `accessMode`, and `storageClass`. Here is an example with the default values:
```yaml
workspaceVolumes:
  allocationStrategy: isolatedPerWorkspace
  size: 12Gi
  storageClass: null  # leaving it null means it will use the cluster default StorageClass
  accessMode: ReadWriteOnce
```

- Renamed the contrib chart to catalog, as we feel this name describes its purpose more clearly.

- Added an optional CronJob that pauses every environment. Configure the values of the platform chart to use it. Here are the default values:
```yaml
environmentScheduler:
  enabled: false  # Change to true to enable
  serviceAccountName: "environment-scheduler"
  clusterRoleName: "environment-scheduler"
  clusterRoleBindingName: "environment-scheduler"
  cronJob:
    name: "environment-scheduler"
    schedule: "0 22 * * *"
    image:
      name: "docker.io/alpine/kubectl"
      tag: "1.34.2"
```

If you enable it with the default values every environment will be paused daily at 22:00.

- Added some extra customization options for the platform, such as the Ingress class and their annotations. Here are the default values:
```yaml
ingress:
  className: nginx
  annotations: {}
```

The internal registry size is also configurable:
```yaml
internalRegistry:
  volumeSize: 50Gi
```

- Some options were included to control the pod placement for the CPS1 server (operator), gateway and internal OCI registry. The defaults are empty:
```yaml
workloads:
  # See https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodeselector
  nodeSelector: {}
  # See https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity
  affinity: {}
  # See https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/
  tolerations: []
```

Here is an example to provision those pods on nodes tainted with `workload=addons:NoSchedule`:
```yaml
workloads:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
          - matchExpressions:
              - key: workload
                operator: In
                values:
                  - addons
  tolerations:
    - key: workload
      operator: Equal
      value: addons
      effect: NoSchedule
```

You can use this to create a node group with smaller nodes to run CPS1 and other cluster addons, while a node group with bigger nodes are available to run the development environments.

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
