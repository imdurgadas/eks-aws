# eks-aws

## Create EKS Cluster (Control Plane) without Worker Nodes.

`eksctl create cluster --name=eks-cluster-1 --region=ap-south-1 --zones=us-south-1a,us-south-1b --without-nodegroup`

## Create and link IAM OIDC Provder for the cluster

Use IAM roles for Kubernetes Service Accounts.

```
eksctl utils associate-iam-oidc-provider --region ap-south-1 --cluster eks-cluster-1 --approve
```


### Create Node Group (Spot Instance Worker Node)

```
eksctl create nodegroup --cluster eks-cluster-1 --region ap-south-1 --instance-types t3a.medium,t3.medium --nodes-volume-size 20 --managed --spot --name eks-cluster-spot-ng --asg-access ----full-ecr-access --appmesh--access --alb-ingress-access --external-dns-access nodes-max 5 --ssh-access --ssh-public-key=kube-demo
``
