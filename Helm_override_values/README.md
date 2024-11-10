


# Overriding Values in Helm

Helm charts come with default values that are defined in a `values.yaml` file. These values control various configurations for your application, such as replica counts, image versions, resource limits, and more. Overriding these values enables you to customize Helm deployments without modifying the chart itself.

## Methods for Overriding Values

There are multiple ways to override values in Helm:

1. **Using Command Line Arguments**
2. **Using a Custom `values.yaml` File**
3. **Combining Multiple Overrides**

### 1. Using Command Line Arguments ```--set```


You can override individual values directly on the command line using the `--set` flag. This approach is helpful for quick overrides, though it can become complex if you need to override many values.

**Example:**

```bash
helm install my-release my-chart --set replicaCount=3 --set image.tag=1.2.3
```

### 2. Using a Custom values.yaml File
```yaml
replicaCount: 3
image:
  repository: my-image-repo
  tag: 1.2.3
resources:
  limits:
    cpu: "500m"
    memory: "512Mi"
```
```bash
helm install my-release my-chart -f my-values.yaml
```

## Helm: Using `--dry-run`, `--debug`, and `helm get`

Helm provides various options to test, troubleshoot, and retrieve information about deployments in Kubernetes. This guide covers three useful commands and flags:
- `--dry-run`: Simulates a Helm command without executing it.
- `--debug`: Provides detailed output to help troubleshoot issues.
- `helm get`: Retrieves information about a specific Helm release.

### `--dry-run` Flag

The `--dry-run` flag simulates a Helm command without making actual changes to the cluster. This is useful for testing and previewing changes before applying them.

### Common Use Cases

1. **Preview Installations**: See the resources that would be created if you install a chart.
2. **Test Upgrades**: Check what changes would occur on an upgrade.
3. **Validate YAML Syntax**: Ensure all templates render correctly before applying them to the cluster.

### Example Usage

```bash
helm install my-release my-chart --dry-run
```
### Using --dry-run with --debug

Combining --dry-run with --debug provides additional information, such as template values and hooks, to help troubleshoot template errors and unexpected output.
```bash
helm install my-release my-chart --dry-run --debug
```
This command will:

- Render templates as usual.
- Display debug output, including variable values and rendered templates.
- Highlight any potential issues or syntax errors in the chart.
