# webb.ai helm-charts

This helm repo is hosted at https://webb-ai.github.io/helm-charts/.

## Installation

```bash
helm repo add webb.ai https://webb-ai.github.io/helm-charts/
helm repo update
helm install webbai-agent webb.ai/webbai-agent -n webbai --create-namespace --set clientID="xxx" --set apiKey="xxx"
```

Get the clientID and apiKey from webb.ai.


## Publish a new chart


```bash
helm package sources/webbai-agent --destination packages
helm repo index . --url https://webb-ai.github.io/helm-charts/ --merge index.yaml
git add .
git commit -m "publish a new chart"

```

## Helm chart parameters

| Parameter | Description | Default |
| --- | --- | --- |
| `clientID` | The client ID to use for authentication with the webb.ai API. This value can be obtained by contacting webb.ai. | `""` |
| `apiKey` | The API key to use for authentication with the webb.ai API. This value can be obtained by contacting webb.ai. | `""` |
| `resourceCollector.image.tag` | The tag of the container image to use for the resource collector. | `v0.4.5` |
| `resourceCollector.kafka.servers` | A comma-separated list of bootstrap servers for Kafka to use for the resource collector. | `""` |
| `resourceCollector.resources.requests.memory` | The amount of memory to request for the resource collector container. | `1000Mi` |
| `resourceCollector.resources.requests.cpu` | The amount of CPU to request for the resource collector container. | `300m` |
| `resourceCollector.resources.limits.memory` | The maximum amount of memory that can be used by the resource collector container. | `2000Mi` |
| `resourceCollector.resources.limits.cpu` | The maximum amount of CPU that can be used by the resource collector container. | `500m` |
| `trafficCollector.image.tag` | The tag of the container image to use for the traffic collector. | `v0.8.3.1` |
| `trafficCollector.resources.requests.memory` | The amount of memory to request for the traffic collector container. | `200Mi` |
| `trafficCollector.resources.requests.cpu` | The amount of CPU to request for the traffic collector container. | `300m` |
| `trafficCollector.resources.limits.memory` | The maximum amount of memory that can be used by the traffic collector container. | `1000Mi` |
| `trafficCollector.resources.limits.cpu` | The maximum amount of CPU that can be used by the traffic collector container. | `500m` |
| `redactEnvVar` | Specifies whether environment variables in containers and initContainers of pods, deployments, daemonsets, statefulsets, job, and cronjobs should be masked before sending to webb.ai. If set to `true`, environment variables will be masked. If set to `false`, environment variables will not be masked. | `false` |

