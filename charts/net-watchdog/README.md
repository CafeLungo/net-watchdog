# net-watchdog

![Version: 0.2.0](https://img.shields.io/badge/Version-0.2.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: latest](https://img.shields.io/badge/AppVersion-latest-informational?style=flat-square)

A Helm chart for watching for a host nic to connectivity, and reboot the host if it's down.

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{"nodeAffinity":{"requiredDuringSchedulingIgnoredDuringExecution":{"nodeSelectorTerms":[{"matchExpressions":[{"key":"kubernetes.io/os","operator":"In","values":["linux"]}]}]}}}` | Default affinity for all nodes |
| fullnameOverride | string | `""` |  |
| image.pullPolicy | string | `"Always"` |  |
| image.repository | string | `"busybox"` |  |
| image.tag | string | `""` |  |
| imagePullSecrets | list | `[]` |  |
| nameOverride | string | `""` |  |
| nodeSelector | object | `{}` |  |
| podAnnotations | object | `{}` |  |
| podLabels | object | `{}` |  |
| podSecurityContext | object | `{}` |  |
| priorityClassName | string | `"system-node-critical"` | Default priority class |
| resources | object | `{"limits":{"cpu":"25m","memory":"8Mi"},"requests":{"cpu":"5m","memory":"1Mi"}}` | Rather minimal resources |
| securityContext.capabilities.drop[0] | string | `"ALL"` |  |
| securityContext.privileged | bool | `true` |  |
| terminationGracePeriodSeconds | int | `5` |  |
| tolerations | list | `[]` |  |
| volumeMounts | list | `[]` |  |
| volumes | list | `[]` |  |
| watchdog.delaySec | int | `60` | How frequently to poll |
| watchdog.interface | string | `"enp1s0"` | Interface to monitor |
| watchdog.maxDownCount | int | `5` | How many down counts before the host is rebooted |
