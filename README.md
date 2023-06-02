# HELM Chart - De Taal Toolbox app

Make sure that you have [Helm](https://helm.sh/docs/intro/install/) and [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) installed on your machine and that you are connected to a Kubernetes cluster.

Create an `traefik-values-override.yaml` file with the following content:

```yaml
additionalArguments:
  - "--providers.kubernetesingress.ingressendpoint.publishedservice=traefik/traefik"
```

Add the Traefik Helm repository :

```bash
helm repo add traefik https://traefik.github.io/charts
```

Update your repository list :

```bash
helm repo update
```

Install Traefik :

```bash
helm install -f traefik-values-override.yaml traefik traefik/traefik -n traefik --create-namespace
```

Install cert-manager :

```bash
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.11.2/cert-manager.yaml
```

### Add the Helm repository

```bash
helm repo add dtt-chart https://rachiid007.github.io/dtt-chart
```

This command adds the repository under the alias dtt-chart. You can replace dtt-chart with any other name of your choice.

### Update your repository list

```bash
helm repo update
```

This command updates your local repository list to reflect the latest changes on remote repositories.

### View the chart list

```bash
helm search repo dtt-chart
```

This command displays the list of charts available in the dtt-chart repository.

### Install the chart

```bash
helm install my-dtt dtt-chart/dtt-chart
```

This command installs the dtt-chart chart in the default namespace. The release name is my-dtt. You can replace my-dtt with any other name of your choice.

### Install the chart with custom values.yaml file

You can find the default values.yaml file [here](https://github.com/Rachiid007/dtt-chart/blob/main/charts/values.yaml).

If you want to override the default values, you can create a custom values.yaml file and use it to install the chart.

For example, if you want to override the default values for the `namespace.name` and `url` parameters, you can create a custom values.yaml file with the following content:

```yaml
namespace:
  name: my-namespace

url: https://my-dtt-subdomain.taaltoolbox.be
```

Then, you can use the following command to install the chart with your custom values.yaml file:

```bash
helm install my-dtt dtt-chart/dtt-chart -f values.yaml
```

### Upgrade the chart

If you want to upgrade the tag of the image used by the frontend deployment, you can use the following command:

```bash
helm upgrade my-dtt dtt-chart/dtt-chart --reuse-values --set=frontend.deployment.image.tag=new_tag
```

This command upgrades the chart with the new tag of the image used by the frontend deployment. The --reuse-values flag reuses the values from the previous installation.

### View releases

```bash
helm list
```

This command displays the list of installed releases.

### Uninstall the chart

```bash
helm uninstall my-dtt
```

### Remove the Helm repository

```bash
helm repo remove dtt-chart
```
