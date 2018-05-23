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

**Step 1:** Build docker images and push them to Azure Container Registry(ACR)
- Create Container Registry (contain images)

		az group create --name myResourceGroup --location eastus    
		az acr create --resource-group myResourceGroup --name {acrName} --sku Basic

- Build .Net core images
	
    	docker-compose build

- Push images to ACR

		az login --tenant {tenantId}
        az acr login --name {ACRname}                
    	docker push {ACRname}.azurecr.io/{imagename}
    
    Ex: 
    
      docker push osdcr.azurecr.io/candidateservice:v5
      or docker push osdcr.azurecr.io/candidateservice (default is use latest version)

**Step 2:** Create Kubernetes Cluster

	az aks create --resource-group {myResourceGroup} --name {myAKSCluster} --node-count 1 --generate-ssh-keys

- Connect with Kubectl


        az aks install-cli
        az aks get-credentials --resource-group myResourceGroup --name myAKSCluster
        kubectl get nodes

- Configure ACR authentication

		CLIENT_ID=$(az aks show --resource-group myResourceGroup --name myAKSCluster --query "servicePrincipalProfile.clientId" --output tsv)
        
		ACR_ID=$(az acr show --name <acrName> --resource-group myResourceGroup --query "id" --output tsv)
        
        az role assignment create --assignee $CLIENT_ID --role Reader --scope $ACR_ID


Deploy sample .Net core solution to Local Kubernetes or AKS
