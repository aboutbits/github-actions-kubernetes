# GitHub Actions Kubernetes

A collection of Kubernetes related GitHub actions.

## Actions

### Setup kubectl and Helm

Setup kubectl and Helm using kubeconfig file.

#### Example

```yaml
  - uses: aboutbits/github-actions-kubernetes/setup-kubectl-and-helm@v3
    with:
      kubeconfig: ${{ secrets.KUBECONFIG }}
```

#### Inputs

The following inputs can be used as `step.with` keys:

| Name           | Required/Default | Description                 |
|----------------|------------------|-----------------------------|
| `kubeconfig`   | required         | The kubeconfig file content |
| `kube-version` | `v1.33.1`        | The version of kubectl      |
| `helm-version` | `v3.17.3`        | The version of Helm         |

### Deploy to Kubernetes using kubectl

Deploy application to a Kubernetes Cluster. Requires Kubernetes to be configured first.

#### Example

```yaml
  - uses: aboutbits/github-actions-kubernetes/kubectl-deploy@v3
    with:
      deployment-file: 'infrastructure/kubernetes.prod.yml'
      namespace-name: ${{ env.NAMESPACE_NAME }}
      deployment-name: ${{ env.DEPLOYMENT_NAME }}
```

#### Inputs

The following inputs can be used as `step.with` keys:

| Name                   | Required/Default     | Description                                |
|------------------------|----------------------|--------------------------------------------|
| `deployment-file`      | required             | Deployment file for kubectl to apply       |
| `namespace-name`       | required             | Kubernetes namespace name                  |
| `deployment-name`      | required             | Kubernetes deployment name                 |
| `working-directory`    | `.`                  | The working directory                      |

### Deploy to Kubernetes using Helm

Deploy an application to a Kubernetes cluster using its Helm chart. Requires Kubernetes to be configured first.

#### Example

```yaml
  - uses: aboutbits/github-actions-kubernetes/helm-deploy@v3
    with:
      helm-chart-version: "1.0.0"
      helm-package: "my-app-chart"
      helm-username: ${{ secrets.HELM_USERNAME }}
      helm-password: ${{ secrets.HELM_PASSWORD }}
      release-name: my-app
      values-file: environments/values-test.yaml
      image-tag: "1.0.42"
      timeout: 5m
      working-directory: ./infrastructure
```

#### Inputs

The following inputs can be used as `step.with` keys:

| Name                 | Required/Default | Description                                                      |
|----------------------|------------------|------------------------------------------------------------------|
| `helm-chart-version` | required         | The version of the Helm chart to pull                            |
| `helm-registry-url`  | required         | The URL of the Helm OCI registry                                 |
| `helm-package`       | required         | The name of the Helm package to pull                             |
| `helm-username`      | required         | The username for authenticating with the Helm registry           |
| `helm-password`      | required         | The password for authenticating with the Helm registry           |
| `helm-protocol`      | `oci://`         | The protocol for pulling Helm charts (e.g., `oci://`)            |
| `release-name`       | required         | The name of the Helm release                                     |
| `namespace`          | required         | The namespace in which to deploy the Helm chart and application. |
| `values-file`        | required         | Path to the Helm values file for customization                   |
| `image-tag`          | `latest`         | The tag of the container image to set                            |
| `timeout`            | `5m`             | The timeout for the Helm command                                 |
| `working-directory`  | `.`              | The working directory where the action commands will operate     |

### Setup PostgreSQL Preview Schema

Sets up a PostgreSQL preview schema by cloning a base schema.

#### Example

```yaml
  - uses: aboutbits/github-actions-kubernetes/setup-postgres-preview-schema@v3
    with:
      configmap-name: my-app-environments
      namespace: my-namespace
      preview-number: ${{ github.event.number }}
```

#### Inputs

The following inputs can be used as `step.with` keys:

| Name              | Required/Default | Description                                |
|-------------------|------------------|--------------------------------------------|
| `configmap-name`  | `app-spring-deployment-env` | Name of the ConfigMap           |
| `namespace`       | required         | Kubernetes namespace                       |
| `preview-number`  | required         | Preview number (PR number)                 |
| `secret-name`     | `app-secrets`    | Name of the secret containing PostgreSQL password |
| `postgres-image`  | `postgres:18`    | PostgreSQL image to use                    |
| `base-schema`     | `main`           | Base schema to copy from                   |
| `db-host-key`     | `DB_HOST`        | Key for DB_HOST in ConfigMap               |
| `db-port-key`     | `DB_PORT`        | Key for DB_PORT in ConfigMap               |
| `db-name-key`     | `DB_NAME`        | Key for DB_NAME in ConfigMap               |
| `db-schema-key`   | `DB_SCHEMA`      | Key for DB_SCHEMA in ConfigMap             |
| `db-username-key` | `DB_USERNAME`    | Key for DB_USERNAME in ConfigMap           |
| `db-password-key` | `DB_PASSWORD`    | Key for DB_PASSWORD in Secret              |

### Teardown PostgreSQL Preview Schema

Drops the PostgreSQL preview schema.

#### Example

```yaml
  - uses: aboutbits/github-actions-kubernetes/teardown-postgres-preview-schema@v3
    with:
      configmap-name: my-app-environments
      namespace: my-namespace
      preview-number: ${{ github.event.number }}
```

#### Inputs

The following inputs can be used as `step.with` keys:

| Name              | Required/Default | Description                                |
|-------------------|------------------|--------------------------------------------|
| `configmap-name`  | `app-spring-deployment-env` | Name of the ConfigMap           |
| `namespace`       | required         | Kubernetes namespace                       |
| `preview-number`  | required         | Preview number (PR number)                 |
| `secret-name`     | `app-secrets`    | Name of the secret containing PostgreSQL password |
| `postgres-image`  | `postgres:18`    | PostgreSQL image to use                    |
| `db-host-key`     | `DB_HOST`        | Key for DB_HOST in ConfigMap               |
| `db-port-key`     | `DB_PORT`        | Key for DB_PORT in ConfigMap               |
| `db-name-key`     | `DB_NAME`        | Key for DB_NAME in ConfigMap               |
| `db-schema-key`   | `DB_SCHEMA`      | Key for DB_SCHEMA in ConfigMap             |
| `db-username-key` | `DB_USERNAME`    | Key for DB_USERNAME in ConfigMap           |
| `db-password-key` | `DB_PASSWORD`    | Key for DB_PASSWORD in Secret              |

## Build & Publish

To build and publish the action, visit the GitHub Actions page of the repository and trigger the workflow "Release Package" manually.

## Information

About Bits is a company based in South Tyrol, Italy. You can find more information about us on [our website](https://aboutbits.it).

### Support

For support, please contact [info@aboutbits.it](mailto:info@aboutbits.it).

### Credits

- [All Contributors](../../contributors)

### License

The MIT License (MIT). Please see the [license file](license.md) for more information.
