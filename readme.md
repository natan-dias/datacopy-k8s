# Datacopy - A Simple Job copy for K8s

This is a simple job to copy data from one PVC to another at the same samespace. Useful for migrations and upgrades.

## Steps

- Change variables to your values:

> $NAMESPACE = Your namespace name
> 
> $PVC-OLD-NAME = Name of the old PVC
>
> $PVC-NEW-NAME = Name of the new PVC

- Run the yaml

> kubectl apply -f datacopy.yml

- Check progress

> kubectl get pod -n $NAMESPACE

