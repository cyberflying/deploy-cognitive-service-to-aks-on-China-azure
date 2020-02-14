# DEPLOY COGNITIVE SERVICE CONTAINER TO AKS ON CHINA AZURE
---
# Create aks cluster
https://docs.azure.cn/aks/kubernetes-walkthrough-portal


# Get cognitive service container

# Create a secret based on existing Docker credentials
kubectl create secret docker-registry <secret-name> --docker-server=containerpreview.azurecr.io --docker-username=<username> --docker-password=<pwd>