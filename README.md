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

Step 1: Build docker images and push them to Azure Container Registry(ACR)
- Create Container Registry (contain images)

		az group create --name myResourceGroup --location eastus
    
		az acr create --resource-group myResourceGroup --name {acrName} --sku Basic

- Build .Net core images
	
    	docker-compose build

- Push images to ACR

		az acr login --name {ACRname}
    
    	docker push {ACRname}.azurecr.io/{imagename}
    
    Ex: 
    
      docker push osdcr.azurecr.io/candidateservice:v5
      or docker push osdcr.azurecr.io/candidateservice (default is use latest version)


Deploy sample .Net core solution to Local Kubernetes or AKS
