# 部署认知服务的容器到China Azure上的AKS群集
---

## 前提条件
* 准备China Azure账号。可以申请[免费试用](https://wd.azure.cn/zh-cn/pricing/1rmb-trial-full)。
* 访问认知服务容器  
目前有些认知服务的容器是公开的，比如LUIS自然语言理解、关键词提前、语言检测以及观点分析等等，有些还处于预览状态，需要[申请](https://docs.microsoft.com/zh-cn/azure/cognitive-services/cognitive-services-container-support)才能获得。申请也非常简单，不需要付费，直接网上填写申请表格即可。

## 环境准备
* [安装Azure CLI](https://docs.azure.cn/zh-cn/cli/install-azure-cli?view=azure-cli-latest)  
建议安装最新版本，本实例要求运行 Azure CLI 2.0.64 版或更高版本。Azure CLI既可以访问China Azure，也可以访问全球Azure。  
访问China Azure需要设置：  
```
az cloud set -n AzureChinaCloud
```
访问全球Azure需要设置：  
```
az cloud set -n AzureCloud
```
* 安装kubectl  
```
az aks install-cli
```

## 创建AKS群集
可以参考[使用Azure门户部署AKS群集](https://docs.azure.cn/aks/kubernetes-walkthrough-portal)，或者[使用Azure CLI创建AKS群集](https://docs.azure.cn/zh-cn/aks/kubernetes-walkthrough)  
下面是具体步骤的截图，供参考：
* 选择Kubernetes Services进行创建![](/img/aks1.png)
* 填写群集名称、区域等基本信息![](/img/aks2.png)
* 认证选项保持默认，启用RBAC![](/img/aks3.png)
* 网络设置可以保持默认Basic。如果需要使用Virtual Nodes则必须使用Advanced网络选项![](/img/aks4.png)
* 其他选项保持默认。创建成功后可查看overview页面![](/img/aks5.png)
* 在insights页面可以看到相关组件的监控状态信息![](/img/aks6.png)
* 创建的AKS集群，需要基础架构相关资源的支撑。比如，VM，存储，网络等等组件，Azure会在AKS cluster创建时将这些底层资源单独创建在另外一个资源组中，这个资源组的名称规则是`MC_<aks resource group name>_<aks name>_<aks location>` ![](/img/aks7.png)

## Get cognitive service container
[Azure 认知服务中的容器](https://docs.microsoft.com/zh-cn/azure/cognitive-services/cognitive-services-container-support#containers-in-azure-cognitive-services)
## Create a secret based on existing Docker credentials
kubectl create secret docker-registry <secret-name> --docker-server=containerpreview.azurecr.io --docker-username=<username> --docker-password=<pwd>