Intsall OIDC provider

```
eksctl utils associate-iam-oidc-provider \
    --region us-east-1 \
    --cluster roboshop-dev \
    --approve

Dowanload IAM policy

curl -o iam-policy.json https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v3.4.0/docs/install/iam_policy.json

Create IAM Policy 

aws iam create-policy \
    --policy-name AWSLoadBalancerControllerIAMPolicy \
    --policy-document file://iam-policy.json

Create service accout & IAM role  . Map above policy

eksctl create iamserviceaccount \
--cluster=roboshop-dev \
--namespace=kube-system \
--name=aws-load-balancer-controller \
--attach-policy-arn=arn:aws:iam::008616580268:policy/AWSLoadBalancerControllerIAMPolicy \
--override-existing-serviceaccounts \
--region us-east-1 \
--approve
