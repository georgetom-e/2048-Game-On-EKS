# 2048-Game-On-EKS
2048 Tile Game Deployed on AWS EKS 


Pre-requisites: 

1. AWS CLI 
2. kubectl 
3. eksctl 


Installation: 


1. EKS cluster setup (fargate): eksctl create cluster --name 2048-game-cluster --region ap-south-1 --fargate

2. kubectl-EKS connection: aws eks update-kubeconfig --region ap-south-1 --name 2048-game-cluster

3. create fargate profile (isolate fargate managed resources): eksctl create fargateprofile --cluster 2048-game-cluster --region ap-south-1 --name alb-2048-game --namespace game-2048

4. create namespace, deployment, pod, service, ingress rule: kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.5.4/docs/examples/2048/2048_full.yaml

5. configure IAM-OIDC provider (for ingress controller - ALB communication): eksctl utils associate-iam-oidc-provider --cluster 2048-game-cluster --approve
