This project contains 11 microservices deployed with kubernetes using Helm charts.

Microservices
1- EmailService - 8080
2- PaymentService - 50051
3- ShippingService - 50051
4- Adservice - 9555
5- CheckoutService - 5050
6- CurrencyService - 7000
7- ProductCatalogService - 3550
8- RecommendationService - 8080
9- CartService - 7070
10- Rredis
11- Frontend - 8080


# STEPS

### Prepare your cluster
 
1. define your enviromental variables

```
export RANDOM_ID ="$(openssl rand -hex 3)"
export RG_GRP="myAKSResourceGroup$RANDOM_ID"
export REGION="westeurope"
export aksCLUSTER_NAME="aksCluster$RANDOM_ID"
export DNS_LABEL="dnslabel$RANDOM_ID"

```

2. create a resource group for the workloads

` az group create --name $RG_GRP --location $REGION ` 


3. create the aks cluster 

```
az aks create \
       --name $aksCLUSTER_NAME \
       --resource-group $RG_GRP \
       --node-count 1 \
       --genarate-ssh-keys

```


4. Run the following commands to command below get download the config file, so kubectl can connect to the cluster

 ```
  az aks get-credentials --resource-group $rRG_GRP --region $REGION --name $aksCLUSTER_NAME 

```

### Install helm on ubuntu using

```
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null

sudo apt-get install apt-transport-https --yes
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list

sudo apt-get update

sudo apt-get install helm

```


verify that helm is installed 
` helm --version `


` helmfile sync`





# REFERENCES

https://helm.sh/docs/intro/cheatsheet/