# Helm Charts

- **Create a Chart**
```bash
helm create my-app-chart
```

```bash
my-app-chart
├── charts
├── Chart.yaml
├── .helmignore
├── templates
│   ├── deployment.yaml
│   ├── _helpers.tpl
│   ├── hpa.yaml
│   ├── ingress.yaml
│   ├── NOTES.txt
│   ├── serviceaccount.yaml
│   ├── service.yaml
│   └── tests
│       └── test-connection.yaml
└── values.yaml

4 directories, 11 files
```

- **.helmignore**:
The .helmignore file in a Helm chart works similarly to a .gitignore file in Git. It specifies files and directories that should be excluded from the chart package when the chart is packaged using the helm package command. This helps reduce the size of the package and excludes unnecessary or sensitive files from being included in the final .tgz file

- **Chart.yaml**:
 is a critical file in a Helm chart that contains metadata about the chart itself. It provides details like the chart’s name, version, and description, and it also defines dependencies if the chart relies on other charts. Helm reads Chart.yaml to understand the chart's structure and to manage deployments, upgrades, and rollbacks.
    - in chart.yml 
        appversion is nothing but docker image version/tag  
    - Can impletemt dependency charts
    - maintainers
```yaml
apiVersion: v2
name: my-webapp
description: A Helm chart for deploying My Web Application
type: application
version: 0.1.0
appVersion: "1.0.0"
keywords:
  - web
  - frontend
  - example
maintainers:
  - name: Alice Smith
    email: alice@example.com
home: "https://example.com"
sources:
  - "https://github.com/example/my-webapp"
dependencies:
  - name: mysql
    version: ">=8.0.0"
    repository: "https://charts.bitnami.com/bitnami"

```
- **values.yaml.**: 
In Helm, values.yaml is a key configuration file used to define default values for the chart. This file contains the customizable parameters for the chart templates, allowing users to set specific values without directly modifying the templates. During deployment, these values are substituted into the template files in the templates/ directory, providing flexibility in how the application is deployed and configured.

```yaml
# Application image settings
image:
  repository: my-application
  tag: "1.0.0"
  pullPolicy: IfNotPresent

# Number of replicas to run for the application
replicaCount: 3

# Service configuration
service:
  type: LoadBalancer
  port: 80

# Application resource limits
resources:
  limits:
    cpu: 500m
    memory: 512Mi
  requests:
    cpu: 250m
    memory: 256Mi

# Environment variables
env:
  - name: NODE_ENV
    value: production
  - name: DEBUG
    value: "false"
```

