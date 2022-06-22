# Kubernetes-deployment Strategies
# Create Spring Boot app
## You can use the sample project which I have in here.

git clone https://github.com/TechPrimers/spring-boot-lazy-init-example.git

### Create Docker image
Command to create docker image using Google JIB plugin

./mvnw com.google.cloud.tools:jib-maven-plugin:build -Dimage=gcr.io/$GOOGLE_CLOUD_PROJECT/spring-boot-example:v1

### Run the Docker image
Command to run the docker image which we created in the previous step

docker run -ti --rm -p 8080:8080 gcr.io/$GOOGLE_CLOUD_PROJECT/spring-boot-example:v1

### Login to the K8s Cluster
Command to login to the K8s cluster from Cloud Shell

gcloud container clusters get-credentials techprimer-cluster-1 --zone us-central1-a

### Kubernetes Commands
List Pods

$ kubectl get pods

List Deployments

$ kubectl get deployments

List Services

$ kubectl get services

Deploy an image

$ kubectl run spring-boot-example --image=gcr.io/$GOOGLE_CLOUD_PROJECT/spring-boot-example:v1 --port=8080

Expose Load Balancer

$ kubectl expose deployment spring-boot-example --type=LoadBalancer

Scale deployments

$ kubectl scale deployment spring-boot-example --replicas=3

K8s YAML Creator
Link to Brandon Potter's YML builder - https://static.brandonpotter.com/kubernetes/DeploymentBuilder.html

# Commands to Create/Update

kubectl apply -f deployment.yml

kubectl apply -f service.yml

Command to retrieve logs

kubectl logs <POD_NAME>

# Pod Name can be retrived using kubectl get pods
## Deployment Strategies
* Recreate
* RollingUpdate
* Blue/Green
* Canary

# Recreate Strategy

kubectl apply -f kube-Recreate.yml

# RollingUpdate Strategy

kubectl apply -f kube-rollingUpdate.yml

# Blue/Green Deployment

## Commands

kubectl apply -f deployment-blue-v1.yml

kubectl apply -f service-blue-v1.yml

kubectl apply -f deployment-green-v2.yml

kubectl apply -f service-green-v2.yml

kubectl apply -f deployment-blue-v2.yml

kubectl apply -f service-blue-v2.yml

kubectl delete deployment.apps/spring-boot-example-v1 service/spring-boot-example-green

# Canary Deployments
## Type 1
## Commands

kubectl apply -f kube-v1.yml

kubectl apply -f deployment-v2.yml

kubectl apply -f service-v1.yml

kubectl apply -f service-v2.yml

## Type 2
## Commands

kubectl apply -f kube-v3.yml

kubectl apply -f ingress.yml

kubectl apply -f ingress-default.yml
