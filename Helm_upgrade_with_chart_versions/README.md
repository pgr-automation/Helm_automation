
```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo list
helm repo update
helm install my-app bitnami/nginx
helm install my-app bitnami/nginx --version "1.20" ## 
helm history my-app
helm status my-app
helm status my-app --show-resources



helm upgrade my-app bitnami/nginx --version "1.20"
```


## Helm Rollback
```bash
# Rollback to previous version
helm rollback RELEASE-NAME 
helm rollback myapp101

# List Helm Release
helm list 

# List Kubernetes Resources Deployed as part of this Helm Release
helm status myapp101 --show-resources

# List Release History
helm history myapp101
```
## Helm Rollback to specific Revision

```bash

helm rollback RELEASE-NAME REVISION
helm rollback myapp101 1

# List Helm Release
helm list 

# List Kubernetes Resources Deployed as part of this Helm Release
helm status myapp101 --show-resources



# List Release History
helm history myapp101
```
