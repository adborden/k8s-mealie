# k8s-mealie

This project provides Kustomize resources for deploying [Mealie](https://mealie.io/) recipe app.

## Usage

Render the manifests with Kustomize and apply them to your cluster:

    kubectl create namespace mealie
    kustomize build github.com/adborden/k8s-mealie.git//mealie | kubectl -n mealie apply -f -

If you need to Kustomize the deployment, you can include this Kustomization in your own:

```yaml
---
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization

namespace: mealie

resources:
  - https://github.com/adborden/k8s-mealie.git//manifests?ref=v1.0.0
```

## Development

### Requirements

- [poetry](https://python-poetry.org/) 2.x
- [kustomize](https://kustomize.io/) 5.x
- [node.js](https://nodejs.org/) LTS
- [GNU Make](https://www.gnu.org/software/make/)

### Development workflow

Render your manifests for inspection.

    make build

Lint the code.

    make lint

Render the Kustomization.

    make test

We use snapshot based testing to validate the rendered manifests. If your tests are failing due to differences, please inspect these carefully. If changes are intentional, update the snapshots.

    make snapshot-update

### Coding conventions

- Follow PEP8 for python
- Unordered lists should be sorted alphabetrically
- Store kustomize resources in a `resources` directory, patches in a `patches` directory, etc.

## Releases

Releases are made automatically by CI on merge. Make sure to use [Conventional Commit](https://www.conventionalcommits.org/) syntax for your commit messages.
