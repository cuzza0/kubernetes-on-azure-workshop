# Deploying Kubernetes on Azure

In this module we are going to install Kubernetes on Azure. The first thing we  
need to do is create a resource group.  

Please note you do not need to use `eastus` you can create a resource group in an region.  

## Create a resource group
Bash: `az group create --name k8s --location eastus`

Powershell: `New-AzResourceGroup -Name k8s -Location eastus`

Next we are going to create the AKS cluster. If you are using a trial account you will need to change the machine size `v1`

## Create your cluster
Bash:
```
az aks create --resource-group k8s \
    --name k8s \
    --generate-ssh-keys \
    --kubernetes-version 1.12.6 \
    --enable-rbac \
    --node-vm-size Standard_DS2_v2
```

Powershell:
```
ssh-keygen -N <password> -f <path>

New-AzAks -ResourceGroupName k8s `
-Name k8s `
-KubernetesVersion 1.12.6 `
-SshKeyValue "<path>" `
-NodeVmSize "Standard_DS2_v2"
```

Next install the `kubectl` binary if you dont already have it installed. Now if you are using cloud shell you can skip this step as it is already installed. For Powershell it is recommended to use the Chocolatey Package Manager, for that follow the installation structions

## If you dont have the kubectl binary installed
Bash: `az aks install-cli`

Powershell: `choco install kubernetes-cli`

## Get your cluster credentials
Bash: `az aks get-credentials --resource-group k8s --name k8s`

Powershell: `Import-AzAksCredential -ResourceGroupName k8s -Name k8s`

## Test your cluster
`kubectl get nodes`  
`kubectl get pods --all-namespaces`
