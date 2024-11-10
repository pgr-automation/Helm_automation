# Helm `--atomic` Flag

The `--atomic` flag in Helm provides an automatic rollback feature that ensures a deployment or upgrade is completed successfully, or, if it fails, is fully rolled back to the previous state. This feature is especially useful for maintaining consistency and stability in your Kubernetes cluster by preventing partial or failed releases.

## Purpose of `--atomic`

The `--atomic` flag adds reliability to Helm deployments by following an all-or-nothing approach:

- **All-or-Nothing Deployment**: With `--atomic`, Helm will ensure that your deployment is fully successful. If any part of the deployment fails, Helm will automatically rollback all changes, leaving no partial resources behind.
  
- **Rollback on Failure**: If any issues arise during the installation or upgrade process (e.g., a pod fails to start or a service doesn't become available), Helm will undo the deployment and revert your cluster to its previous state.

## How It Works

### Installation
When using `--atomic` with `helm install`, Helm will:
1. Attempt to deploy all resources in the chart (e.g., Deployments, Services, ConfigMaps).
2. Confirm that each resource is successfully created and running.
3. If any resource fails (e.g., a pod crashes or encounters an error), Helm will delete the partially created resources and report the installation as failed.

### Upgrade
Similarly, using `--atomic` with `helm upgrade` will:
1. Attempt to apply all new resources and updates to existing resources.
2. If any new resource fails or an updated resource becomes unavailable, Helm will roll back the entire upgrade, restoring the previous release version.

## Key Benefits of `--atomic`

Using `--atomic` in Helm has several benefits:
- **Consistency**: Ensures no incomplete or partially failed resources are left in your cluster.
- **Reliability**: Automates rollback on failure, simplifying the deployment process.
- **Ease of Use**: Great for CI/CD pipelines, where automated rollbacks prevent unstable releases from reaching production.

## Usage Examples

You can use `--atomic` with both `install` and `upgrade` commands:

```bash
# Using --atomic with install
helm install my-release my-chart --atomic

# Using --atomic with upgrade
helm upgrade my-release my-chart --atomic
```
## Limitations

While --atomic is powerful, it has some limitations:

-  No Granular Rollback Control: --atomic performs a complete rollback, which may not be desirable if you only want to troubleshoot or debug specific resources.
-  Additional Time Requirement: Rollbacks add time to the deployment process, as Helm waits for Kubernetes resources to be created, validated, and, if necessary, deleted  upon failure.