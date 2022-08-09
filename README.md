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
- [OpenShift Console](https://console-openshift-console.apps.smaug.na.operate-first.cloud/)

- [ArgoCd Console](https://argocd.operate-first.cloud/applications)


### Apicurio Registry

- [Apicurio Registry Openshift Project](https://console-openshift-console.apps.smaug.na.operate-first.cloud/k8s/cluster/projects/apicurio-apicurio-registry)

- [Apicurio Registry ArgoCD Application](https://argocd.operate-first.cloud/applications/registry-smaug?resource=)

- [Apicurio Registry Instance](https://apicurio-registry-apicurio-apicurio-registry.apps.smaug.na.operate-first.cloud/)

- [Apicurio Registry Multitenant UI](http://apicurio-registry-mt-ui-mt-apicurio-apicurio-registry.apps.smaug.na.operate-first.cloud/)

### API Designer

- [API Designer Openshift Project](https://console-openshift-console.apps.smaug.na.operate-first.cloud/k8s/cluster/projects/api-designer)

- [API Designer ArgoCD Application](https://argocd.operate-first.cloud/applications/api-designer-smaug?resource=)

- [API Designer POC UI](https://api-designer-poc.apps.smaug.na.operate-first.cloud/)

- [ADS UI](https://ads-ui.apps.smaug.na.operate-first.cloud/)

- [Studio Editors UI](https://studio-editors.apps.smaug.na.operate-first.cloud/?demo)

# Docs and SOPs
Please follow the below links for more information on:-
- [Apicurio Operate-First set up](docs/apicurio-operate-first-setup.md)
- [Apicurio Registry deployment](docs/registry-deployment.md)
- [Api Designer deployment](docs/api-designer-deployment.md)

