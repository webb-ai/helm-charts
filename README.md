# webb.ai helm-charts

This helm repo is hosted at https://webb-ai.github.io/helm-charts/.

## Installation

```bash
helm repo add webb.ai https://webb-ai.github.io/helm-charts/
helm repo update
helm upgrade --install webbai-agent webb.ai/webbai-agent -n webbai --create-namespace --set-string clientID="xxx" --set apiKey="xxx"
```

Get the clientID and apiKey from webb.ai.


## Publish a new chart

Package the helm chart locally:

```bash
git pull
git pull --tags
helm package sources/webbai-agent --destination packages
```

Testing the local change:

```bash
helm upgrade --install webbai-agent packages/webbai-agent-0.2.0.tgz -n webbai
```

Release it:

```bash
helm repo index . --url https://webb-ai.github.io/helm-charts/ --merge index.yaml
git add .
git commit -m "publish a new chart"
git push
cr upload --owner webb-ai --git-repo helm-charts  --package-path packages --skip-existing
```

## Helm chart parameters

| Parameter | Description | Default |
| --- | --- | --- |
| `clientID` | The client ID to use for authentication with the webb.ai API. This value can be obtained by contacting webb.ai. | `""` |
| `apiKey` | The API key to use for authentication with the webb.ai API. This value can be obtained by contacting webb.ai. | `""` |
| `resourceCollector.kafka.servers` | A comma-separated list of bootstrap servers for Kafka to use for the resource collector. | `""` |
| `resourceCollector.resources.requests.memory` | The amount of memory to request for the resource collector container. | `1000Mi` |
| `resourceCollector.resources.requests.cpu` | The amount of CPU to request for the resource collector container. | `300m` |
| `resourceCollector.resources.limits.memory` | The maximum amount of memory that can be used by the resource collector container. | `2000Mi` |
| `resourceCollector.resources.limits.cpu` | The maximum amount of CPU that can be used by the resource collector container. | `500m` |
| `trafficCollector.resources.requests.memory` | The amount of memory to request for the traffic collector container. | `200Mi` |
| `trafficCollector.resources.requests.cpu` | The amount of CPU to request for the traffic collector container. | `300m` |
| `trafficCollector.resources.limits.memory` | The maximum amount of memory that can be used by the traffic collector container. | `1000Mi` |
| `trafficCollector.resources.limits.cpu` | The maximum amount of CPU that can be used by the traffic collector container. | `500m` |
| `trafficCollector.tolerations` | Tolerations for traffic collector. |
| `redactEnvVar` | Specifies whether environment variables in containers and initContainers of pods, deployments, daemonsets, statefulsets, job, and cronjobs should be masked before sending to webb.ai. If set to `true`, environment variables will be masked. If set to `false`, environment variables will not be masked. | `false` |

