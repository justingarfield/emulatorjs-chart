# emulatorjs

Deploys an emulatorjs pod into Kubernetes.

![Version: 0.0.1](https://img.shields.io/badge/Version-0.0.1-informational?style=flat-square) ![AppVersion: 2022.01.27](https://img.shields.io/badge/AppVersion-2022.01.27-informational?style=flat-square) 

## Source Code

* <https://github.com/justingarfield/emulatorjs-chart>
* <https://hub.docker.com/r/linuxserver/emulatorjs>
* <https://github.com/linuxserver/emulatorjs>

## IPFS Warning

emulatorjs uses something called the [InterPlanetary File System (IPFS)](https://ipfs.io/). Due to the way this distributed peer-to-peer file-system works, it may open connections to IP addresses that are considered hostile / infected / compromised. This in-turn will cause malware scanners (e.g. MalwareBytes) to throw MANY blocked connection warnings. This is normal behavior and it's up to you to decide whether to suppress these warnings, not run emulatorjs, and/or enforce more strict container / network settings. (I personally run my instance in its own little "isolated jail", so that if something malicious gets pulled down over the IPFS file-system, I could care less, as I'll just blow away the release and redeploy it)

## Installation

```shell
helm repo add justingarfield https://justingarfield.github.io/emulatorjs-chart/
helm repo update
```
## Uninstallation

To uninstall/delete the `my-release` deployment (NOTE: `--purge` is default behaviour in Helm 3+ and will error):

```shell
helm delete --purge my-release
```

## Configuration

The following table lists the configurable parameters of the emulatorjs chart and the default values.

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| antiaff.avoidRelease | string | `"emulatorjs1"` | Here you can set the emulatorjs release (you set in `helm install <releasename> ...`) you want to avoid |
| antiaff.enabled | bool | `false` | set to true to enable antiaffinity (example: 2 emulatorjs in the same cluster) |
| antiaff.strict | bool | `true` | Here you can choose between preferred or required |
| customVolumes.config | object | `{}` | any volume type can be used here |
| customVolumes.enabled | bool | `false` | set this to true to enable custom volumes |
| env.ipfsPeeringPort | int | `4001` |  |
| env.managementUIPort | int | `3000` |  |
| env.pgid | int | `1000` |  |
| env.publicUIPort | int | `80` |  |
| env.puid | int | `1000` |  |
| env.subfolder | string | `"/"` |  |
| env.tz | string | `"Europe/London"` |  |
| hostNetwork | string | `"false"` | should the container use host network |
| hostname | string | `""` | hostname of pod |
| image.pullPolicy | string | `"IfNotPresent"` | the pull policy |
| image.repository | string | `"linuxserver/emulatorjs"` | the repostory to pull the image from |
| image.tag | string | `"latest"` | the docker tag, if left empty it will get it from the chart's appVersion |
| ingress | object | `{"annotations":{},"enabled":false,"hosts":["chart-example.local"],"path":"/","tls":[]}` | Configuration for the Ingress |
| ingress.annotations | object | `{}` | Annotations for the ingress |
| ingress.enabled | bool | `false` | Generate a Ingress resource |
| maxSurge | int | `1` | The maximum number of Pods that can be created over the desired number of `ReplicaSet` during updating. |
| maxUnavailable | int | `1` | The maximum number of Pods that can be unavailable during updating |
| persistentVolumeClaims | object | `{"config":{"accessModes":["ReadWriteOnce"],"annotations":{},"enabled":false,"size":"500Mi"},"data":{"accessModes":["ReadWriteOnce"],"annotations":{},"enabled":false,"size":"500Mi"}}` | `spec.PersitentVolumeClaim` configuration |
| persistentVolumeClaims.config.annotations | object | `{}` | Annotations for the `PersitentVolumeClaim` |
| persistentVolumeClaims.config.enabled | bool | `false` | set to true to use pvc |
| persistentVolumeClaims.data.annotations | object | `{}` | Annotations for the `PersitentVolumeClaim` |
| persistentVolumeClaims.data.enabled | bool | `false` | set to true to use pvc |
| podAnnotations | object | `{}` | Additional annotations for pods |
| podDnsConfig.enabled | bool | `true` |  |
| podDnsConfig.nameservers[0] | string | `"127.0.0.1"` |  |
| podDnsConfig.nameservers[1] | string | `"1.1.1.1"` |  |
| podDnsConfig.policy | string | `"None"` |  |
| probes | object | `{"liveness":{"enabled":true,"failureThreshold":3,"initialDelaySeconds":0,"periodSeconds":10,"successThreshold":1,"timeoutSeconds":1},"readiness":{"enabled":true,"failureThreshold":3,"initialDelaySeconds":0,"periodSeconds":10,"successThreshold":1,"timeoutSeconds":1}}` | Probes configuration |
| probes.liveness.enabled | bool | `true` | Generate a liveness probe |
| probes.readiness.enabled | bool | `true` | Generate a readiness probe |
| replicaCount | int | `1` | The number of replicas |
| service.annotations | object | `{}` | Annotations for the service |
| service.externalTrafficPolicy | string | `"Local"` | `spec.externalTrafficPolicy` for the service |
| service.ipfsPeering.nodePort | int | `30001` |  |
| service.ipfsPeering.port | int | `4001` |  |
| service.loadBalancerIP | string | `""` | A fixed `spec.loadBalancerIP` for the service |
| service.managementUI.nodePort | int | `30000` |  |
| service.managementUI.port | int | `3000` |  |
| service.publicUI.nodePort | int | `30080` |  |
| service.publicUI.port | int | `80` |  |
| service.type | string | `"NodePort"` | `spec.type` for the Service |
| strategyType | string | `"RollingUpdate"` | The `spec.strategyTpye` for updates |
| virtualHost | string | `"emulatorjs"` |  |

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| Justin Garfield | helm-charts@jgarfield.com |  |

## Credits

This chart was heavily influenced by the pihole chart available @ https://github.com/MoJo2600/pihole-kubernetes/tree/master/charts/pihole. I really like how they've handled support for the multiple ways of handling networking and storage aspects of their template, and decided to follow suit. Thanks to that team for all the hard-work that helped breathe life into this one!
