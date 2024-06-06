# React App Deployment with Docker, Kubernetes, and HPA for Autoscaling

This repository contains the steps to create, containerize, and deploy a React Quiz application using Docker, Kubernetes, and HPA for autoscaling

## Prerequisites
* Docker installed on your machine
* Minikube installed for Kubernetes
* kubectl installed for managing Kubernetes clusters

# Steps to Deploy the React App
## 1. Create a React App
Create a new React application using the following command:
```bash
npx create-react-app my-quiz-app
```

## 2. Dockerize the React App
### i) Install Docker

Download and install Docker from the [Docker website.](https://docs.docker.com/desktop/install/windows-install/) 

### ii) Create a Dockerfile in the App Directory

Create a Dockerfile in the root directory of your React app: `React-Docker-Kubernetes/Reactquiz-Docker/dockerfile
`
### iii) Create a .dockerignore File

Create a .dockerignore file in the root directory of your React app: `React-Docker-Kubernetes/Reactquiz-Docker/.dockerignore
`


### iv) Build and Run the Docker Container

Use the following commands to build and run your Docker container:

#### Build the Docker image
```bash
docker build .
```
#### List Docker images and copy the image ID
```bash
docker images
```

#### Run the Docker container (replace <image-id> with the actual image ID)
```bash
docker run -p 3000:3000 <image-id>
```

You can now access your React app in the browser at http://localhost:3000.

## 3. Set Up Kubernetes with Minikube

### i) Install Minikube and kubectl

Download and install Minikube from the [Minikube website.](https://minikube.sigs.k8s.io/docs/start/?arch=%2Fwindows%2Fx86-64%2Fstable%2F.exe+download)

Download and install kubectl from the [Kubernetes website.](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/)

## 4. Deploy to Kubernetes

### i) Create Kubernetes YAML Files

[React-Docker-Kubernetes
/kubernetes files
](https://github.com/Saisamarth21/React-Docker-Kubernetes/tree/master/kubernetes%20files)


Use the following commands to apply the YAML files and manage your Kubernetes resources:


#### Apply the YAML files
```bash
kubectl apply -f file.yaml
```
#### List the pods
```bash
kubectl get pods
```

#### List the services
```bash
kubectl get services
```

#### Get the Minikube IP address
```bash
minikube ip
```

Access your app in the browser using the Minikube IP address and the port number from the service.

### ii) Set Up Horizontal Pod Autoscaling

To use autoscaling, you need to apply the metrics server. Navigate to the metrics_server directory and apply all files: `React-Docker-Kubernetes/Metric files/
`

```bash
kubectl apply -f 
```
Create the HPA (Horizontal Pod Autoscaler) YAML files.

[React-Docker-Kubernetes
/kubernetes files
](https://github.com/Saisamarth21/React-Docker-Kubernetes/tree/master/kubernetes%20files)



#### Apply the YAML files
```bash
kubectl apply -f file.yaml
```
#### Check CPU and memory utilization
```bash
kubectl top nodes
```

#### List the HPA resources
```bash
kubectl get hpa
```

#### Generate load to test autoscaling (replace <hpa-demo-deployment> with your deployment name)
```bash
kubectl run -i --tty load-generator --rm --image=busybox --restart=Never -- /bin/sh -c "while sleep 0.01; do wget -q -O- http://<hpa-demo-deployment>; done"
```

## 5. Push Docker Image to DockerHub


#### Push the Docker image to DockerHub
```bash
docker push <docker-username>/<app-name>
```

#### Pull the Docker image from DockerHub
```bash
docker pull saisamarth21/reactquiz-docker
```

#### Pull the Docker image from GitHub Packages
```bash
docker pull ghcr.io/saisamarth21/react-docker:latest
```

