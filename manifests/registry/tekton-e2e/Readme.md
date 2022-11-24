
Before applying those resources you nedd to create a secret with the credentials:

```bash
kubectl create secret generic e2e-registry-secret --from-literal=username=<username> --from-literal=password=<password>
```
