# GitHub Actions Kubernetes

A collection of Kubernetes related GitHub actions.

## Actions

### Setup DigitalOcean

Setup Digital-Ocean CLI and configure Kubernetes.

#### Example

```yaml
  - uses: aboutbits/github-actions-kubernetes/do-setup-kubectl@v2
    with:
      digital-ocean-token: ${{ secrets.DIGITALOCEAN_TOKEN }}
      cluster-name: ${{ env.CLUSTER_NAME }}
```

#### Inputs

The following inputs can be used as `step.with` keys:

| Name                     | Required/Default   | Description                     |
|--------------------------|--------------------|---------------------------------|
| `digital-ocean-token`    | required           | Digital Ocean access token      |
| `cluster-name`           | required           | Kubernetes cluster name         |


### Deploy to Kubernetes using kubectl

Deploy application to a Kubernetes Cluster. Requires Kubernetes to be configured first.

#### Example

```yaml
  - uses: aboutbits/github-actions-kubernetes/kubectl-deploy@v2
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

Deploy an application to a Kubernetes cluster using its Helm diagram. Requires Kubernetes to be configured first.

#### Example

```yaml
  - uses: aboutbits/github-actions-kubernetes/helm-deploy@v2
    with:
      release-name: my-app
      chart-directory: my-chart
      image-tag: "1.0.0"
      values-file: environments/values-test.yaml
      timeout: 5m
      working-directory: ./infrastructure
```

#### Inputs

The following inputs can be used as `step.with` keys:

| Name                | Required/Default | Description                        |
|---------------------|------------------|------------------------------------|
| `release-name`      | required         | The name of the Helm release       |
| `values-file`       | required         | Path to the Helm values file       |
| `working-directory` | `.`              | The working directory              |
| `chart-directory`   | `.`              | Root directory of the helm diagram |
| `image-tag`         | `latest`         | Tag of the container image         |
| `timeout`           | `5m`             | Timeout for the Helm command       |

## Versioning

In order to have a versioning in place and working, create lightweight tags that point to the appropriate minor release versions.

Creating a new minor release:

```bash
git tag v2
git push --tags
```

Replacing an already existing minor release:

```bash
git tag -d v2
git push origin :refs/tags/v2
git tag v2
git push --tags
```

## Information

About Bits is a company based in South Tyrol, Italy. You can find more information about us on [our website](https://aboutbits.it).

### Support

For support, please contact [info@aboutbits.it](mailto:info@aboutbits.it).

### Credits

- [All Contributors](../../contributors)

### License

The MIT License (MIT). Please see the [license file](license.md) for more information.
