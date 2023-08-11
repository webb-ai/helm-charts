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