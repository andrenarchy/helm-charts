# vaultwarden

Helm chart originally based on a chart from [k8s-at-home](https://github.com/k8s-at-home/charts).

## Source Code

* <https://github.com/dani-garcia/vaultwarden>

## Requirements

Kubernetes: `>=1.16.0-0`

## Dependencies

| Repository | Name | Version |
|------------|------|---------|
| https://charts.bitnami.com/bitnami | mariadb | 11.0.14 |
| https://charts.bitnami.com/bitnami | postgresql | 11.6.12 |
| https://library-charts.k8s-at-home.com | common | 4.5.2 |

## TL;DR

```console
helm repo add andrenarchy https://k8s-at-home.com/charts/
helm repo update
helm install vaultwarden andrenarchy/vaultwarden
```

## Installing the Chart

To install the chart with the release name `vaultwarden`

```console
helm install vaultwarden andrenarchy/vaultwarden
```

## Uninstalling the Chart

To uninstall the `vaultwarden` deployment

```console
helm uninstall vaultwarden
```

The command removes all the Kubernetes components associated with the chart **including persistent volumes** and deletes the release.

## Configuration

Read through the [values.yaml](./values.yaml) file. It has several commented out suggested values.
Other values may be used from the [values.yaml](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common/values.yaml) from the [common library](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common).

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

```console
helm install vaultwarden \
  --set env.TZ="America/New York" \
    andrenarchy/vaultwarden
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart.

```console
helm install vaultwarden andrenarchy/vaultwarden -f values.yaml
```

## Custom configuration

The Vaultwarden chart requires the `/config` folder to exist. In order to provide this, some type of storage needs to be implemented.
For testing purposes, the following config snippet will work:

````yaml
persistence:
  config:
    enabled: true
    type: emptyDir
````

## Values

**Important**: When deploying an application Helm chart you can add more values from our common library chart [here](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common)

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| env | object | See below | environment variables. See [image docs](https://github.com/dani-garcia/vaultwarden/blob/main/.env.template) for more details. |
| env.DATA_FOLDER | string | `"config"` | Config dir |
| image.pullPolicy | string | `"IfNotPresent"` | image pull policy |
| image.repository | string | `"vaultwarden/server"` | image repository |
| image.tag | string | chart.appVersion | image tag |
| ingress.main | object | See values.yaml | Enable and configure ingress settings for the chart under this key. |
| mariadb.enabled | bool | `false` |  |
| persistence | object | See values.yaml | Configure persistence settings for the chart under this key. |
| postgresql.enabled | bool | `false` |  |
| service | object | See values.yaml | Configures service settings for the chart. Normally this does not need to be modified. |
| strategy.type | string | `"Recreate"` |  |
