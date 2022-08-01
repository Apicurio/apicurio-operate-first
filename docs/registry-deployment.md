## Overview
Currently the `manifests/registry/base` folder define a basic Service Registry deployement, that could work as is.

While `overlay_multitenancy` includes the instructions to add all the resources needed to run [Limitador](https://github.com/3scale-labs/limitador/), including the instruction to patch the `Deployment` definition in the `base` folder to add a Sidecar Envoy Proxy container.

The folder `prod` represents what will be deployed to Operate First cluster.


## Local Verification
To verify what is the output of the applied overlay you can run this command:

```bash
cd manifests/registry
oc kustomize prod | tee effective-manifest.yaml
```

If you’re using kustomize as a standalone CLI, you’ll instead run:

```bash
cd manifests/registry
kustomize build prod | tee effective-manifest.yaml
```

The output is the concatenation of all the YAML documents for all of the resources we specified along with the applied overlay, patches, common labels etc.


## Multitenancy enabled deployment

The `overlay_multitenancy` contains configuration files for deploying Apicurio Registry with multitenancy enabled.

```bash
oc apply -k ./manifests/registry/overlay_multitenancy/
```

## Ingresses for local testing

If you are using Kind for testing kubernetes locally in your computer, you can use manifests in `local_testing` for configuring ingresses to Apicurio Registry and Tenant Manager.

```bash
oc apply -k ./manifests/registry/local_testing/
```

