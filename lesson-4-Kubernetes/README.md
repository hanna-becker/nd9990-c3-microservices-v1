# Monolith to Microservices at Scale Project

Find the project code in the 'exercise' directory.

Find screenshots in the screenshots directory.

## Creating the cluster
For creating the k8s cluster in AWS, I installed kops and used this command for creating a cluster with 1 master and 9 worker nodes:
```bash
kops create cluster --name=hannabecker.k8s.local --state=s3://hannabecker-kops-state-store --zones=eu-central-1a --node-count=9 --node-size=t2.micro --master-count=1 --master-size=t2.micro
```

## Deploying to the cluster
The steps for deploying the app to the cluster are automated in the '.travis.yml' file. Please refer to this file for details. It applies the following steps:
* populate environment variables with the ones saved in DockerHub
* build docker images
* push them to DockerHub
* deploy the app's services and environment to the cluster
 
The only thing I deploy manually is the env-secret, as it contains sensitive data. 

## Accessing the app locally
To access the running application locally, I use the following port-forwarding commands:
* kubectl port-forward service/reverseproxy 8080:8080
* kubectl port-forward service/frontend 8100:8100

The app will then be available under http://localhost:8100/.
