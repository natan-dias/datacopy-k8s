# Datacopy - A Simple Job copy for K8s

This is a simple job to copy data from one PVC to another at the same samespace. 
Very useful for migrations and upgrades and tests.

## Requirements

- OLD and NEW PVC need to be created first

## Steps

- Change variables to your values:

> $NAMESPACE = Your namespace name
> 
> $PVC_OLD_NAME = Name of the old PVC
>
> $PVC_NEW_NAME = Name of the new PVC

- Run the yaml

> kubectl apply -f datacopy.yml

- Check progress

> kubectl get pod -n $NAMESPACE -w

When the JOB is done, POD will have the "completed" status:

> datacopy--1-7q2rj          0/1     Completed           0          18s

## Extra - Correct way to remove a PVC with "Retain" policy

https://kubernetes.io/docs/concepts/storage/persistent-volumes/#reclaiming

- Remove finalizer from metadata

> kubectl patch pvc NAME-OF-PVC -n NAMESPACE -p '{"metadata":{"finalizers":null}}'

- Delete PVC

> kubectl delete pvc NAME-OF-PVC -n NAMESPACE

- Check PV status released

> kubectl get pv
>
> NAME-OF-PV     100Mi      RWX            Retain           Released   namespace/NAME-OF-PVC

- Remove PV

> kubectl delete pv NAME-OF-PV

