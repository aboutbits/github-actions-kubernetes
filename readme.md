# GitHub Actions Kubernetes

A collection of Kubernetes related GitHub actions.

## Actions

### Setup DigitalOcean

Setup Digital-Ocean CLI and configure Kubernetes.

#### Example

```yaml
  - uses: aboutbits/github-actions-kubernetes/do-setup-kubectl@v1
    with:
      digital-ocean-token: ${{ secrets.DIGITALOCEAN_TOKEN }}
      cluster-name: ${{ env.CLUSTER_NAME }}
```

#### Inputs

Following inputs can be used as `step.with` keys

| Name                     | Required/Default   | Description                     |
|--------------------------|--------------------|---------------------------------|
| `digital-ocean-token`    | required           | Digital Ocean access token      |
| `cluster-name`           | required           | Kubernetes cluster name         |


### Deploy to Kubernetes

Deploy application to a Kubernetes Cluster. Requires Kubernetes to be configured first.

#### Example

```yaml
  - uses: aboutbits/github-actions-kubernetes/deploy@v1
    with:
      deployment-file: 'infrastructure/kubernetes.prod.yml'
      namespace-name: ${{ env.NAMESPACE_NAME }}
      deployment-name: ${{ env.DEPLOYMENT_NAME }}
```

#### Inputs

Following inputs can be used as `step.with` keys

| Name                 | Required/Default   | Description                               |
|----------------------|--------------------|-------------------------------------------|
| `deployment-file`    | required           | Deployment file for kubectl to apply      |
| `namespace-name`     | required           | Kubernetes namespace name                 |
| `deployment-name`    | required           | Kubernetes deployment name                |


## Versioning

In order to have a versioning in place and working, create lightweight tags that point to the appropriate minor release versions.

Creating a new minor release:

```bash
git tag v1
git push --tags
```

Replacing an already existing minor release:

```bash
git tag -d v1
git push origin :refs/tags/v1
git tag v1
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
