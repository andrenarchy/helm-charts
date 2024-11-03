# wmbusmeters

Read the wired or wireless mbus protocol to acquire utility meter readings.

## Source Code

* <https://github.com/wmbusmeters/wmbusmeters>

## Requirements

Kubernetes: `>=1.16.0-0`

## Dependencies

| Repository | Name | Version |
|------------|------|---------|
| https://library-charts.k8s-at-home.com | common | 4.5.2 |

## TL;DR

```console
helm repo add andrenarchy https://andrenarchy.github.io/helm-charts/
helm repo update
helm install wmbusmeters andrenarchy/wmbusmeters
```

## Installing the Chart

To install the chart with the release name `wmbusmeters`

```console
helm install wmbusmeters andrenarchy/wmbusmeters
```

## Uninstalling the Chart

To uninstall the `wmbusmeters` deployment

```console
helm uninstall wmbusmeters
```

The command removes all the Kubernetes components associated with the chart **including persistent volumes** and deletes the release.

## Configuration

Read through the [values.yaml](./values.yaml) file. It has several commented out suggested values.
Other values may be used from the [values.yaml](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common/values.yaml) from the [common library](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common).

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

```console
helm install wmbusmeters \
  --set env.TZ="America/New York" \
    andrenarchy/wmbusmeters
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart.

```console
helm install wmbusmeters andrenarchy/wmbusmeters -f values.yaml
```

## Custom configuration

**IMPORTANT NOTE:** a radio device must be accessible on the node where this pod runs, in order for this chart to function properly.

First, you will need to mount your radio device into the pod, you can do so by adding the following to your values:

```yaml
additionalVolumeMounts:
  - name: usb
    mountPath: /path/to/device

additionalVolumes:
  - name: usb
    hostPath:
      path: /path/to/device
```

Second you will need to set a nodeAffinity rule, for example:

```yaml
affinity:
  nodeAffinity:
    requiredDuringSchedulingIgnoredDuringExecution:
      nodeSelectorTerms:
      - matchExpressions:
        - key: app
          operator: In
          values:
          - wmbus-radio
```

... where a node with an attached radio device is labeled with `app: wmbus-radio`

If you are getting errors, that the device cannot be opened when starting wmbusmeters, try uncommenting the privileged flag:

```
securityContext:
  privileged: true
```

## Values

**Important**: When deploying an application Helm chart you can add more values from our common library chart [here](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common)

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` | Affinity constraint rules to place the Pod on a specific node. [[ref]](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#affinity-and-anti-affinity) |
| image.pullPolicy | string | `"IfNotPresent"` | image pull policy |
| image.repository | string | `"wmbusmeters/wmbusmeters"` | image repository |
| image.tag | string | `"1.17.1"` | image tag |
| persistence | object | See values.yaml | Configure persistence settings for the chart under this key. |
| persistence.usb | object | See values.yaml | Configure a hostPathMount to mount a USB device in the container. |
| securityContext.privileged | bool | `nil` | Privileged securityContext may be required if USB controller is accessed directly through the host machine |
| service | object | See values.yaml | Configures service settings for the chart. Normally this does not need to be modified. |
