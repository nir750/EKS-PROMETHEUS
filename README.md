# EKS-PROMETHEUS
deploy EKS cluster running prometheus

# Make sure to install and configure AWSCLI in your computer 
here you can find instructions:   
https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html

# deploy EKS cluster
deploy the file eksctl.yml using this command
eksctl create cluster -f eksctl.yml

# Deploy Prometheus
kubectl create namespace prometheus

helm install prometheus prometheus-community/prometheus \
    --namespace prometheus \
    --set alertmanager.persistentVolume.storageClass="gp2" \
    --set server.persistentVolume.storageClass="gp2"

kubectl port-forward -n prometheus deploy/prometheus-server 8080:9090
