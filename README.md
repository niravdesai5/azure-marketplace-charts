# The Bitnami Library for Kubernetes

Popular applications, provided by [Bitnami](https://bitnami.com), ready to launch on Azure Kubernetes Service (AKS) using [Kubernetes Helm](https://github.com/helm/helm). Find all the available applications in the [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/).

## TL;DR

```bash
$ helm repo add azure-marketplace https://marketplace.azurecr.io/helm/v1/repo
$ helm search azure-marketplace
```

## Before you begin

### Provision an Azure Kubernetes Cluster with AKS

The quickest way to setup a Kubernetes cluster is wit `az`, the [Microsoft Azure command-line interface](https://cloud.google.com/container-engine/). If you don't have `az`, [install it using these instructions](https://docs.bitnami.com/azure/faq/administration/install-az-cli/) or use the Azure Portal Console.

Follow the steps below to provision a Kubernetes Cluster with AKS. Refer to our [started guide](https://docs.bitnami.com/azure/get-started-charts-marketplace) for more details:

```bash
$ az login
$ az account set --subscription "SUBSCRIPTION-NAME"
$ az group create --name aks-resource-group --location eastus
$ az aks create --name aks-cluster --resource-group aks-resource-group --generate-ssh-keys
```
The above command creates a new resource group and cluster named `aks-cluster`. Then, install and configure `kubectl` with the credentials to the new AKS cluster, as shown below:

```bash
$ az aks get-credentials --name aks-cluster --resource-group aks-resource-group
```

### Install Helm

Helm is a tool for managing Kubernetes charts. Charts are packages of pre-configured Kubernetes resources.

To install Helm, refer to the [Helm install guide](https://github.com/helm/helm#install) and ensure that the `helm` binary is in the `PATH` of your shell.

```bash
$ kubectl create serviceaccount -n kube-system tiller
$ kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller
$ helm init --service-account tiller
```

The above command creates a ServiceAccount and a ClusterRoleBinding for Tiller and initializes Helm in the cluster.

### Add Repo

Helm Charts are available via the Azure Marketplace public repository.

```bash
$ helm repo add azure-marketplace https://marketplace.azurecr.io/helm/v1/repo
$ helm search azure-marketplace
```

Use the following command to deploy a chart, such as WordPress:

```bash
$ helm install azure-marketplace/wordpress
```

### Using Helm

Once you have installed the Helm client and initialized the Tiller server, you can deploy a Bitnami Helm Chart into a Kubernetes cluster.

Please refer to the [Quick Start guide](https://github.com/helm/helm/blob/master/docs/quickstart.md) if you wish to get running in just a few commands, otherwise the [Using Helm Guide](https://github.com/helm/helm/blob/master/docs/using_helm.md) provides detailed instructions on how to use the Helm client to manage packages on your Kubernetes cluster.

Useful Helm Client Commands:
* View available charts: `helm search`
* Install a chart: `helm install stable/<package-name>`
* Upgrade your application: `helm upgrade`

# License

Copyright (c) 2018 Bitnami

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
