# Helm_automation

# Helm: Kubernetes Package Manager

Helm is a powerful package manager for Kubernetes that helps manage Kubernetes applications using **charts** — collections of files that describe a set of Kubernetes resources. Helm simplifies the deployment, upgrade, and maintenance of applications by packaging Kubernetes resources into reusable, customizable charts.

## Key Components of Helm

### 1. Charts
Charts are Helm packages containing the resources necessary to run an application on Kubernetes. Each chart typically includes:
   - **Templates**: YAML files for Kubernetes resources, using Go templating syntax.
   - **`values.yaml`**: Default configuration values that can be overridden.
   - **`Chart.yaml`**: Metadata about the chart, including name, version, and description.
   - **Dependencies**: Charts your application may rely on, enabling modular design.

### 2. Releases
Each installation of a chart on a Kubernetes cluster is called a **release**. Helm uniquely identifies each release by name, so you can have multiple releases of the same chart running independently.

### 3. Repositories
Helm charts are stored in repositories, which serve as app stores for Helm charts. Public repositories like [Helm Hub](https://artifacthub.io/) and [Bitnami](https://bitnami.com/stacks/helm) provide a variety of ready-to-use charts. You can also create private repositories.

## Key Helm Commands

| Command                             | Description                                                          |
|-------------------------------------|----------------------------------------------------------------------|
| `helm install <release> <chart>`    | Installs a chart, creating a new release.                            |
| `helm upgrade <release> <chart>`    | Updates an existing release with new configurations or chart version. |
| `helm rollback <release> <revision>`| Rolls back to a previous release version.                            |
| `helm uninstall <release>`          | Deletes a release and its associated resources.                      |
| `helm repo add <name> <url>`        | Adds a new repository.                                               |
| `helm repo update`                  | Updates the local repository index.                                  |
| `helm search repo <name>`           | Searches for charts in the added repositories.                       |

## Why Use Helm?

Helm streamlines Kubernetes application management, especially for complex, multi-service applications. Key advantages include:

1. **Version Control**: Helm tracks each release change, making rollbacks straightforward.
2. **Configuration Management**: Customize deployments with `values.yaml`.
3. **Modularity**: Use dependencies to build modular applications.
4. **Automated Lifecycle Management**: Helm automates upgrades, rollbacks, and testing.
5. **Repeatability**: Helm charts ensure consistency across environments.

## Getting Started with Helm: Nginx Example

Let's install an Nginx web server using Helm.

### Step 1: Add a Repository

Add the official stable repository:

```bash
helm repo add stable https://charts.helm.sh/stable
helm repo update
```
### Step 2: Install the Nginx Chart
Install an Nginx release named my-nginx from the stable repository:
```bash
helm install my-nginx stable/nginx
```
### Step 3: List Helm Releases

Verify that the release was created by listing all Helm releases:
```bash
helm list
```

### Step 4: Upgrade the Release

Suppose you want to change the service type to LoadBalancer. First, create a custom values.yaml file with the following content:
```bash
service:
  type: LoadBalancer
```
Then upgrade the release using this new configuration:
```bash
helm upgrade my-nginx stable/nginx -f custom-values.yaml
```
### Step 5: Rollback if Necessary

If you need to rollback to a previous release version, you can do so using the following command:
```bash
helm rollback my-nginx 1
```
The 1 represents the revision number.
