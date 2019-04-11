# Terraform + Amazon EKS

## Preparation

TODO: AWS account and CLI

TODO: Terraform

## Deploying Your Cluster

```bash
terraform init
terraform plan
terraform apply
```

## Controlling Your EKS Cluster With kubectl

### Install kubectl

You will need kubectl installed on your local workstation.  Refer to the [Kubernetes documentation](https://kubernetes.io/docs/tasks/tools/install-kubectl/) for step-by-step instructions for installing kubectl on your operating system.

### Install aws-iam-authenticator

The aws-iam-authenticator is an authentication adapter that enables kubectl to authenticate to your EKS cluster using AWS credentials such as those in your ~/.aws/credentials file or obtained via an Instance Role.  The authenticator is available as a binary for Windows, Linux and macOS, and simply needs to be placed in your system PATH.

For example on Linux:

```bash
wget https://amazon-eks.s3-us-west-2.amazonaws.com/1.12.7/2019-03-27/bin/linux/amd64/aws-iam-authenticator

chmod 755 aws-iam-authenticator

mv aws-iam-authenticator /usr/local/bin
```

For more details and other operating systems refer to the [AWS documentation](https://docs.aws.amazon.com/eks/latest/userguide/install-aws-iam-authenticator.html).

### Export kubectl Config For EKS

kubectl obtains configuration settings from ~/,kube/config.  We can automatically add entries to that configuration file using the AWS CLI - for example:

```bash
aws eks --region ap-southeast-1 update-kubeconfig --name terraform-eks
```

Note you will need to ensure that the region and name are correct for your cluster.  If you get an error stating that update-kubeconfig is an unknown sub-command for EKS, you will need to upgrade to the latest AWS CLI version.

For a full explanation and other options refer to the [AWS documentation](https://docs.aws.amazon.com/eks/latest/userguide/create-kubeconfig.html).

### Use kubectl

You should now be able to use kubectl to control your cluster:

```bash
root@24d9cdfde46c:~# kubectl get namespaces
NAME          STATUS   AGE
default       Active   21m
kube-public   Active   21m
kube-system   Active   21m
```

