> # THIS DOCUMENT IS ARCHIVED

# Apicurio Operate First set up

This document describes what is the setup in operate-first to enable the deployment the manifests in this repository.

<br>

## This repository
This repository contains a set of kubernetes manifests that are organized using kustomize.

<br>

## Operate First Cluster
Operate First initiative has multiple openshift clusters and uses ArgoCD to manage each of those clusters.

Apicurio projects are onboarded to the `smaug` cluster


### Namespace
Our namespaces `apicurio-apicurio-registry` and `api-designer` can be found here [https://github.com/operate-first/apps/blob/master/cluster-scope/base/core/namespaces/]

#### Openshift cluster
And this namespace is created in `smaug` cluster because it's defined here [https://github.com/operate-first/apps/blob/master/cluster-scope/overlays/prod/moc/smaug/kustomization.yaml]

<br>

## Argo CD
ArgoCD is a kubernetes operator to enable GitOps workloads. ArgoCD is deployed in a kubernetes cluster but can deploy applications to many kubernetes clusters.

### Apicurio AppProject
For the ArgoCD part, first an `AppProject` is required, this thing grants permissions to argocd to deploy things to apicurio projects namespaces in the `smuag` cluster.

Our `AppProject` definition is here [https://github.com/operate-first/apps/blob/master/argocd/overlays/moc-infra/projects/apicurio-registry.yaml]

### Apicurio ArgoCD Applications
After this we create the argocd `Application`.This thing is were GitOps starts for us and our application deployments. An `Application` points to a git repository and triggers deployments on changes to the remote git repository.

Our `Application` definitions are here [https://github.com/operate-first/apps/tree/master/argocd/overlays/moc-infra/applications/envs/moc/smaug/apicurio]

### App-of-apps
Operate first is using a pattern called app-of-apps that means they are instructing each one of their clusters with all the applications they have to deploy by using a main argocd application. This main application points to a directory where all the applications that have to be deployed are located. We need to make sure that the ArgoCD applications that we create are tracked by this app-of-apps.

The app-of-apps for the `smaug` cluster is defined here [https://github.com/operate-first/apps/blob/master/argocd/overlays/moc-infra/applications/app-of-apps/app-of-apps-smaug.yaml]



