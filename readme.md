# GitHub Actions Kubernetes

A collection of GitHub actions for Kubernetes.

## Setup DigitalOcean
Setup Digital-Ocean CLI and configure Kubernetes.

### Example

```yaml
  - uses: aboutbits/github-actions-kubernetes/setup-digital-ocean@v1
    with:
      cluster-name: ${{ env.TEST_CLUSTER_NAME }}
      digital-ocean-token: ${{ secrets.DIGITALOCEAN_TOKEN }}
```

## Deploy to Kubernetes
Deploy application to a Kubernetes Cluster. Requires Kubernetes to be configured first.

### Example

```yaml
  - uses: aboutbits/github-actions-kubernetes/deploy-to-kubernetes@v1
    with:
      environment: 'test'
      namespace-name: ${{ env.NAMESPACE_NAME }}
      deployment-name: ${{ env.DEPLOYMENT_NAME }}
```

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
