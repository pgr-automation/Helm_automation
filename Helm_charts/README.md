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
