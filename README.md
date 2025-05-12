# ArgoCD Applications Repository

This repository contains Kubernetes application manifests and Helm charts intended to be deployed via [ArgoCD](https://argo-cd.readthedocs.io/en/stable/) using `ApplicationSet`.

## Structure

The repository is organized into environment-specific folders:

    /bootstrap
    /platform
    /preprod
    /prod


Each folder contains one or more applications structured to be compatible with ArgoCD `ApplicationSet` generators such as `Git` or `Directory`.

## Deployment Workflow

During the bootstrap process of the cluster management machine (using Ansible), this repository is cloned and ArgoCD `ApplicationSet` objects are applied. These ApplicationSets automatically discover and deploy the applications into their respective clusters or namespaces.

- **Bootstrap tools** (e.g., CAPI, cert-manager) are located in the `/bootstrap` folder.
- **Platform tools** (e.g., Vault, Backstage, Prometheus, Grafana, ArgoCD) are located in the `/platform` folder.
- **Pre-production** apps are under `/preprod`. (e.g., Loki agent for log collection and metrics scrapping, kyverno for policy-as-code)
- **Production** apps are under `/prod`.

## Requirements

- A running instance of ArgoCD in the cluster
- `ApplicationSet` controller enabled
- Ansible automation to apply `ApplicationSet` objects from this repo
