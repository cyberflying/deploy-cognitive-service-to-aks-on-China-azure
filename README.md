# 部署认知服务的容器到China Azure上的AKS群集
---
# 创建AKS群集
可以参考[使用Azure portal部署AKS群集](https://docs.azure.cn/aks/kubernetes-walkthrough-portal)  
下面是具体步骤的截图，供参考：
![](/img/aks1.png)
![](/img/aks2.png)
![](/img/aks3.png)
![](/img/aks4.png)
![](/img/aks5.png)
![](/img/aks6.png)
![](/img/aks7.png)
# Get cognitive service container

# Create a secret based on existing Docker credentials
kubectl create secret docker-registry <secret-name> --docker-server=containerpreview.azurecr.io --docker-username=<username> --docker-password=<pwd>