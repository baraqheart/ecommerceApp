This project contains 11 microservices deployed with kubernetes using deployments and service without Helm.

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
10- Rredis -6379
11- Frontend - 8080

# STEPS
 
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

try this, to verify cluster is running fine

` kubectl get nodes `

deploy and get your application running
` kubectl create ns microservices `

` kubectl apply -f deploy-svc/  -n microservices`

` kubectl get pods `

# REFERENCES







