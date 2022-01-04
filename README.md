# EKS_TF

# EKS deployment:



## Config aws-cli:

Creating an IAM account and add then configuring aws-cli to use this IAM account by running and typing neccessery data:

```sh
aws configure
```

## EKS 🔌:

### Installing EKS 🔥 :

Running `init` command to download all modules for Terraform:

```
terraform init
```

Next step is to deploy the EKS cluster

```
terraform apply
```


### Connect kubectl to the cluster 🔌

The following command will configure the local kubectl to connect to the eks cluster.

```
aws eks --region us-east-2 update-kubeconfig --name  my-cluster
```

### If we need to uninstalling EKS :

```
terraform destroy
```

## Redis:

### Installing the cluster 🔥 :

To deploy the redis cluster to the EKS we will use the redis-cluster chart: https://github.com/bitnami/charts/tree/master/bitnami/redis

Adding repo
```
helm repo add bitnami https://charts.bitnami.com/bitnami
```

And installing
```
helm install redis-cluster bitnami/redis
```

### Check the cluster:

Checking if the Redis pod deployed in the previous step is running.

```
helm list
```

To check the running pods:

```
kubectl get pod
```

Enter the created pod with kubectl exec.

```
kubectl exec -it redis-cluster-master-0  -- redis-cli
```

### Uninstalling the cluster :

To uninstall/delete the redis-cluster deployment:

```
$ helm delete redis-cluster
```

## Backup :

To install backup task running the following command:

```
helm install backup cronjob
```
FYI - my first backup solution was locally, without S3 
