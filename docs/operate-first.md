# Apicurio Operate First set up

This document describes what is the setup in operate-first to enable the deployment the manifests in this repository.

## This repository
This repository contains a set of kubernetes manifests that are organized using kustomize.

## Argo CD
ArgoCD is a kubernetes operator to enable GitOps workloads. ArgoCD is deployed in a kubernetes cluster but can deploy applications to many kubernetes clusters.

## Operate First
Operate First initiative has multiple openshift clusters and uses ArgoCD to manage each of those clusters.
Apicurio organization is onboarded to operate-first and has a namespace `apicurio-apicurio-registry` created in the cluster `smaug` cluster.

### Show me:

#### Namespace
Our namespace `apicurio-apicurio-registry` is defined here [https://github.com/operate-first/apps/blob/master/cluster-scope/base/core/namespaces/apicurio-apicurio-registry/namespace.yaml]

#### Openshift cluster
And this namespace is created in `smaug` cluster because it's defined here [https://github.com/operate-first/apps/blob/master/cluster-scope/overlays/prod/moc/smaug/kustomization.yaml]

#### App-of-apps
Operate first is using a pattern called app-of-apps that means they are instructing each one of their clusters with all the applications they have to deploy by using a main argocd application, this main application points to a directory where all the applications that have to be deployed are located. The app-of-apps four the `smaug` cluster is defined here [https://github.com/operate-first/apps/blob/master/argocd/overlays/moc-infra/applications/app-of-apps/app-of-apps-smaug.yaml]

#### Apicurio AppProject
For the ArgoCD part first an `AppProject` is required, this thing grants permissions to argocd to deploy things to `apicurio-apicurio-registry` in `smuag` cluster.
Our `AppProject` definition is here [https://github.com/operate-first/apps/blob/master/argocd/overlays/moc-infra/projects/apicurio-registry.yaml]

#### Apicurio ArgoCD Application
After this we create the argocd `Application`, this thing is were GitOps starts for us and our applications, an `Application` points to a git repository and triggers deployments on changes to the remote git repository.
Our `Application` definition is here [https://github.com/operate-first/apps/blob/master/argocd/overlays/moc-infra/applications/envs/moc/smaug/apicurio/registry.yml]