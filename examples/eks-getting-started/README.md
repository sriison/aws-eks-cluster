# EKS Getting Started Guide Configuration

This is the full configuration from https://www.terraform.io/docs/providers/aws/guides/eks-getting-started.html

See that guide for additional information.

NOTE: This full configuration utilizes the [Terraform http provider](https://www.terraform.io/docs/providers/http/index.html) to call out to icanhazip.com to determine your local workstation external IP for easily configuring EC2 Security Group access to the Kubernetes master servers. Feel free to replace this as necessary.


Initializing and create EKS cluster
terraform init
terraform apply  

# Generate kubeconfig and configmap for adding worker nodes
terraform output kubeconfig > ./kubeconfig
terraform output config_map_aws_auth > ./config_map_aws_auth.yaml

# Apply configmap for worker nodes to join the cluster
export KUBECONFIG=./kubeconfig
kubectl apply -f ./config_map_aws_auth.yaml
kubectl get nodes --watch
