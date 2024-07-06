# Kubectl

```bash title="Cleanup old contexts and clusters"
kubectl config get-contexts -o name

kubectl config get-contexts -o name | grep 'old-context' | xargs -n 1 kubectl config delete-context

kubectl config get-clusters -o name

kubectl config get-clusters -o name | grep 'old-cluster' | xargs -n 1 kubectl config delete-cluster

kubectl config get-users -o name

kubectl config delete-user USERNAME
```
