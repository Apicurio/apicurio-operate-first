# Manifests for OpenShift

This repo contains the Manifests files we are using to Operate First cluster:

OpenShift Console: [https://console-openshift-console.apps.zero.massopen.cloud]
Service Registry Instance: [http://apicurio-registry-apicurio-apicurio-registry.apps.zero.massopen.cloud/]

The project uses [`kustomization`](https://kubernetes.io/docs/tasks/manage-kubernetes-objects/kustomization/) and in particular the `Overlay` functionality, that allows to define basic configuration and a collection of patches(overlays) we can apply on the basic definitions.

Currently the `base` folder define a basic Service Registry deployement, that could work as is.
While `overlay_limitador` includes the instructions to add all the resources needed to run [Limitador](https://github.com/3scale-labs/limitador/), including the instruction to patch the `Deployment` definition in the `base` folder to add a Sidecar Envoy Proxy container.

To apply the `kustomization` command locally, to verify what is the output of the applied overlay you can run this command:

```bash
cd manifests/registry
oc get -k ./overlay_limitador/ -o yaml | tee log.txt
```
