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
#### How values.yaml Works with Templates
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ .Release.Name }}-app
spec:
  replicas: {{ .Values.replicaCount }}
  template:
    spec:
      containers:
        - name: app
          image: {{ .Values.image.repository }}:{{ .Values.image.tag }}
          env:
            - name: NODE_ENV
              value: {{ .Values.env.NODE_ENV }}
          resources:
            {{- toYaml .Values.resources | nindent 12 }}
```

- **charts folder**
In a Helm chart, the charts folder is a directory where Helm stores chart dependencies. Dependencies are other Helm charts that this chart relies on, often reusable components like databases, message queues, or other microservices. By including dependencies in the charts folder, Helm makes it easier to deploy complex applications with multiple components.

- Purpose of the charts Folder

The charts folder allows for modular and composable chart development. Instead of defining all resources in a single chart, you can reference and include other charts as dependencies. This approach promotes reusability and simplifies the management of complex applications that rely on multiple components.
#### How Dependencies Work
```bash
# Chart.yaml
apiVersion: v2
name: my-app
version: 1.0.0

dependencies:
  - name: redis
    version: ">=5.0.0"
    repository: "https://charts.bitnami.com/bitnami"
  - name: mysql
    version: ">=8.0.0"
    repository: "https://charts.bitnami.com/bitnami"
```

This example specifies that my-app depends on the Redis and MySQL charts from Bitnami.
Managing Dependencies with helm dependency

Helm uses the helm dependency command to manage dependencies:

    - helm dependency update: This command downloads the dependencies specified in Chart.yaml and stores them in the charts folder. This process fetches .tgz packages (Helm chart archives) of the dependencies.

    - helm dependency build: This command also downloads dependencies, building them according to the Chart.yaml.
#### Structure of the charts Folder
```bash
my-app/
├── Chart.yaml
├── values.yaml
├── charts/
│   ├── redis-5.0.0.tgz
│   └── mysql-8.0.0.tgz
├── templates/
│   └── deployment.yaml
```