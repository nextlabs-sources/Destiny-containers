## Kubernetes for the whole setup

### Pre-requisite For Registry credentials

#### Minikube

Modify file `registry-secret.yaml` and run:

```shell
kubectl apply -f registry-secret.yaml
```

### Steps

#### Create StorageClass Object when deploy to AWS (for PVC claims)

```shell
# the aws PVC needs to have ebs-storageclass deployed first
kubectl apply -f ebs-storageclass.yaml
```

#### Create Ingress Controller (traefik)

```shell
kubectl apply -f traefik.yaml
```

1. Create namespace

```shell
kubectl apply -f namespace.yaml
```

2. Create configMap

```shell
kubectl apply -f cc-configMap.yaml
```

3. Create secrets

```shell
kubectl apply -f cc-secrets.yaml
# then the certificates as secret (replace {namesapce} with actual value)
kubectl --namespace {namespace} create secret generic cc-certificates --from-file=cc-certificates
```

4. Create database deployment (optional) and run init jobs.

```shell
# create database deployment
kubectl apply -f postgres.yaml
# run init job
kubectl apply -f init-job.yaml
```

5. Create the whole deployment

```shell
kubectl apply -f cc-stack.yaml
```

