# Azure Pipelines Agent
[Azure Pipelines Agent](https://github.com/woozchucky/azure-pipelines-agent) is self-hosted agent that you can run in a container with Docker. The agent is pre-installed with Docker inside of it and .NET SDK 8.0.

[![Release](https://img.shields.io/github/release/woozchucky/azure-pipelines-agent.svg?style=flat-square)](https://github.com/woozchucky/azure-pipelines-agent/releases/latest)
[![Docker Image](https://img.shields.io/docker/image-size/woozchucky/azure-pipelines-agent/latest?style=flat-square)](https://hub.docker.com/r/woozx/azure-pipelines-agent)
[![Docker Pulls](https://img.shields.io/docker/pulls/woozchucky/azure-pipelines-agent.svg?style=flat-square)](https://hub.docker.com/r/woozx/azure-pipelines-agent)
[![license](https://img.shields.io/github/license/woozchucky/azure-pipelines-agent.svg?style=flat-square)](LICENSE)

> Supports `amd64`, `arm` and `arm64`

## Agent Version

This image will automatically pull and install the latest Azure DevOps version at startup.

## Deployment

The Azure Pipeliens agent can be deployed in Docker using either `docker run` or `docker compose` or in Kubernetes using Helm (recommended).

#### Deployment in `docker`

```
docker run -d -e AZP_AGENT_NAME="<agent name>" -e AZP_URL="https://dev.azure.com/<your org.>" -e AZP_POOL="<agent pool>" -e AZP_TOKEN="<PAT>" woozx/azure-pipelines-agent
```


#### Deployment in `Kubernetes` using `Helm`

Use Helm to install the latest released chart:
```shellsession
$ helm repo add woozchucky https://woozchucky.github.io/helm-charts
$ helm repo update
$ helm upgrade --install azure-pipelines-agent woozchucky/azure-pipelines-agent
```

You can customize the values of the helm deployment by using the following Values:

| Parameter                     | Description                                                                                       | Default                                                  |
|-------------------------------|---------------------------------------------------------------------------------------------------|----------------------------------------------------------|
| `nameOverride`                | Overrides release name                                                                            | `""`                                                     |
| `fullnameOverride`            | Overrides release fullname                                                                        | `""`                                                     |
| `image.repository`            | Container image repository                                                                        | `emberstack/azure-pipelines-agent`                       |
| `image.tag`                   | Container image tag                                                                               | `""` (same version as the chart)                         |
| `image.pullPolicy`            | Container image pull policy                                                                       | `Always` if `image.tag` is `latest`, else `IfNotPresent` |
| `pipelines.url`               | The Azure base URL for your organization                                                          | `""`                                                     |
| `pipelines.pat.value`         | Personal Access Token (PAT) used by the agent to connect.                                         | `""`                                                     |
| `pipelines.pat.secretRef`     | The reference to the secret storing the Personal Access Token (PAT) used by the agent to connect. | `""`                                                     |
| `pipelines.pool`              | Agent pool to which the Agent should register.                                                    | `""`                                                     |
| `pipelines.agent.mountDocker` | Enable to mount the host `docker.sock`                                                            | `false`                                                  |
| `pipelines.agent.workDir`     | The work directory the agent should use                                                           | `_work`                                                  |
| `serviceAccount.create`       | Create ServiceAccount                                                                             | `true`                                                   |
| `serviceAccount.name`         | ServiceAccount name                                                                               | _release name_                                           |
| `serviceAccount.clusterAdmin` | Sets the service account as a cluster admin                                                       | _release name_                                           |
| `resources`                   | Resource limits                                                                                   | `{}`                                                     |
| `nodeSelector`                | Node labels for pod assignment                                                                    | `{}`                                                     |
| `tolerations`                 | Toleration labels for pod assignment                                                              | `[]`                                                     |
| `affinity`                    | Node affinity for pod assignment                                                                  | `{}`                                                     |
| `additionalEnv`               | Additional environment variables for the agent container.                                         | `[]`                                                     |
| `extraVolumes`                | Additional volumes for the agent pod.                                                             | `[]`                                                     |
| `extraVolumeMounts`           | Additional volume mounts for the agent container.                                                 | `[]`                                                     |
| `initContainers`              | InitContainers for the agent pod.                                                                 | `[]`                                                     |