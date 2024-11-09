The helm upgrade command with the --set option allows you to modify specific values of a Helm chart during an upgrade without changing the values file. The syntax is as follows:

```bash
helm upgrade <release-name> <chart> --set key1=value1,key2=value2,...
```
Example Usage

Suppose you have a Helm release named my-release and you're upgrading it with new values for specific keys:
```bash
helm upgrade my-release my-chart --set image.tag=1.2.3,replicaCount=3
```
In this example:

 ```
image.tag=1.2.3 changes the image tag used in the deployment.
replicaCount=3 sets the number of replicas to 3.
```
### Setting Nested Values

If you have nested values, you can specify them with dots (.):
```bash
helm upgrade my-release my-chart --set resources.limits.cpu=200m
```
This example sets the cpu limit under resources.limits.
Using Arrays

### For array values, use brackets ({}):
```bash
helm upgrade my-release my-chart --set service.ports[0].port=80
```
Additional Tips

    For complex configurations, use --set-file to pass a file for specific keys.
    Alternatively, use --values or -f to specify a custom values file if multiple changes are needed.

This approach makes it easy to modify values temporarily or for a specific environment without altering the base chart values.