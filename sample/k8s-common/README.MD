## Kubernetes for the whole setup

### Pre-requisite For Registry credentials

#### Minikube

Modify file `registry-secret.yaml` and run:

```shell
kubectl apply -f registry-secret.yaml
```

#### AWS

Need to create storageclass

```shell
kubectl apply -f ebs-storageclass.yaml
```

### Steps

#### Create Ingress Controller (traefik) (different file for different provider)

```shell
kubectl apply -f traefik.yaml
```

1. Create namespace

```shell
# (replace {namesapce} with actual value)
kubectl create namespace {namespace}
```

1. Create configMap

```shell
# First replace {external_dns} with actual external dns
kubectl --namespace {namespace} apply -f cc-configMap.yaml
```

2. Create secrets

```shell
kubectl --namespace {namespace} apply -f cc-secrets.yaml
# then the certificates as secret (replace {namesapce} with actual value)
kubectl --namespace {namespace} create secret generic cc-certificates --from-file=cc-certificates
```

3. Create database deployment (optional) and run init jobs.

```shell
# create database deployment
kubectl --namespace {namespace} apply -f postgres.yaml
# run init job
kubectl --namespace {namespace} apply -f dbinit-job.yaml
```

4. Create the whole deployment

```shell
kubectl --namespace {namespace} apply -f cc-stack.yaml
```

5. Create the ingress

```shell
# First replace {external_dns} with actual external dns
kubectl --namespace {namespace} apply -f ingress.yaml
```
