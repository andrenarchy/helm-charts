# photoprism

PhotoPrism® is a server-based application for browsing, organizing and sharing your personal photo collection

Helm chart originally based on a chart from [k8s-at-home](https://github.com/k8s-at-home/charts).

## Source Code

* <https://github.com/photoprism/photoprism>
* <https://hub.docker.com/r/photoprism/photoprism>

## Requirements

Kubernetes: `>=1.16.0-0`

## Dependencies

| Repository | Name | Version |
|------------|------|---------|
| https://charts.bitnami.com/bitnami | mariadb | 11.0.14 |
| https://library-charts.k8s-at-home.com | common | 4.5.2 |

## TL;DR

```console
helm repo add andrenarchy https://andrenarchy.github.io/helm-charts/
helm repo update
helm install photoprism andrenarchy/photoprism
```

## Installing the Chart

To install the chart with the release name `photoprism`

```console
helm install photoprism andrenarchy/photoprism
```

## Uninstalling the Chart

To uninstall the `photoprism` deployment

```console
helm uninstall photoprism
```

The command removes all the Kubernetes components associated with the chart **including persistent volumes** and deletes the release.

## Configuration

Read through the [values.yaml](./values.yaml) file. It has several commented out suggested values.
Other values may be used from the [values.yaml](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common/values.yaml) from the [common library](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common).

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

```console
helm install photoprism \
  --set env.TZ="America/New York" \
    andrenarchy/photoprism
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart.

```console
helm install photoprism andrenarchy/photoprism -f values.yaml
```

## Custom configuration

N/A

## Values

**Important**: When deploying an application Helm chart you can add more values from our common library chart [here](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common)

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| env | object | See below | environment variables. See [image docs](https://docs.photoprism.org/getting-started/config-options/) for more details. |
| env.GID | string | `nil` | Sets GID Photoprism runs under. |
| env.PHOTOPRISM_ADMIN_PASSWORD | string | `"please-change"` | Initial admin password. **BE SURE TO CHANGE THIS!** |
| env.PHOTOPRISM_DATABASE_DRIVER | string | `"sqlite"` | Database driver (sqlite, mysql) |
| env.PHOTOPRISM_DATABASE_NAME | string | `"photoprism"` | Database schema name |
| env.PHOTOPRISM_DATABASE_PASSWORD | string | `"photoprism"` | Database user password |
| env.PHOTOPRISM_DATABASE_SERVER | string | `"photoprism-mariadb:3306"` | Database host incl. port |
| env.PHOTOPRISM_DATABASE_USER | string | `"photoprism"` | Database user name |
| env.PHOTOPRISM_ORIGINALS_PATH | string | `"/photoprism/originals"` | Photoprism originals path |
| env.PHOTOPRISM_PUBLIC | string | `"false"` | Disable authentication / password protection |
| env.PHOTOPRISM_STORAGE_PATH | string | `"/photoprism/storage"` | Photoprism storage path |
| env.TZ | string | `"UTC"` | Set the container timezone |
| env.UID | string | `nil` | Sets UID Photoprism runs under. |
| env.UMASK | string | `nil` | Sets UMASK. |
| image.pullPolicy | string | `"IfNotPresent"` | image pull policy |
| image.repository | string | `"photoprism/photoprism"` | image repository |
| image.tag | string | chart.appVersion | image tag |
| ingress.main | object | See values.yaml | Enable and configure ingress settings for the chart under this key. |
| mariadb | object | See values.yaml | Enable and configure mariadb database subchart under this key.    For more options see [mariadb chart documentation](https://github.com/bitnami/charts/tree/master/bitnami/mariadb) |
| persistence | object | See values.yaml | Configure persistence settings for the chart under this key. |
| service | object | See values.yaml | Configures service settings for the chart. |

