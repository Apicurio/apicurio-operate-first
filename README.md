# Operate First
Operate First is a community of developers, operators, and others — site reliability engineers (SRE), data scientists, Open Source practitioners, and so forth — who believe in promoting Open Source approach to operations.

Open Source software is widely available, but it faces an operations-barrier when bringing it to a production environment.

Proprietary services have attempted to address this barrier, but they undermine the Open Source development model because lessons learned from operating the code are invisible to the Open Source developers.
To overcome this operations barrier in an Open Source way, we must switch to an Open Source-like approach to operations, or Open Operations (Open Ops).

Open Ops means developers and operators collaborating Openly to apply a product's operational considerations right back into the code itself. The result is an Open Source service.

For More information on operate-first, please visit https://www.operate-first.cloud/


# This Repository
This repository holds the manifests files that are used for deploying the apicurio projects on the operate-first cluster. The manifest files for each project are organized under the manifests folder.

The project uses [kustomize](https://kubernetes.io/docs/tasks/manage-kubernetes-objects/kustomization/) and in particular the `Overlay` functionality, that allows to define basic configuration and a collection of patches(overlays) we can apply on the base definitions.

Apicurio Operate First deployments uses [Argo CD](https://argo-cd.readthedocs.io/en/stable/) to enable GitOps and continuous deployments. Hence, any changes made to the manifest files will automatically be applied to the project deployments.

# Useful links

### Generic

- [Cluster Details](https://github.com/3scale/platform/blob/master/docs/projects/engineering/dev-ocp-mas.md)
  
- [OpenShift Console](https://console-openshift-console.apps.dev-eng-ocp4-mas.dev.3sca.net/)

- [ArgoCd Console](https://gitops.apps.dev-eng-ocp4-mas.dev.3sca.net/applications)

### Backstage

- [Backstage Instance](https://backstage-rhaf-apicurio-registry.apps.dev-eng-ocp4-mas.dev.3sca.net/)
  


