# Kubernetes With Dotnet Core & Angular

### Documentations
- https://docs.microsoft.com/en-us/azure/aks/tutorial-kubernetes-prepare-app 
- https://kubernetes.io/docs/tutorials/kubernetes-basics/create-cluster/cluster-intro


### Tools
- Docker toolbox
- Azure CLI
- Helm CLI
- kubectl

### Step by step

Step 1: Build docker images and push them to Azure Container Registry
- Create Container Registry (contain images)

	**az group create --name myResourceGroup --location eastus**
    
	**az acr create --resource-group myResourceGroup --name <acrName> --sku Basic**
- 


Deploy sample .Net core solution to Local Kubernetes or AKS
