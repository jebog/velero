# Installation Process

We use `velero` as namespace

## Create your s3 compatible object storage secret

```ini
[default]
aws_access_key_id = minio
aws_secret_access_key = minio123
```

Replace this value in `credentials.velero` then:

```bash
kubectl create secret generic cloud-credentials --from-file cloud=credentials.velero --dry-run client -o yaml > secrets.yaml
```

## For Openshift

```bash
oc adm policy add-scc-to-user privileged -z velero -n velero
oc annotate namespace velero openshift.io/node-selector=""
```

Edit restic.yaml

```yaml
securityContext:
    privileged: true
```

## Install

```bash
oc apply -k .
```


