# Nginx-Ingress-Controller-Kubernetes-Manifests
deploying Nginx controllers using YAML manifests.
If your Kubernetes cluster does not have access to the internet, you can still install nginx ingress controller by following these steps:

• Download the nginx ingress controller YAML file from the official GitHub repository: https://github.com/kubernetes/ingress-nginx/tree/master/deploy/static/provider/baremetal/deploy.yaml

# Also, here is the one-liner to deploy all the objects.
https://github.com/kubernetes/ingress-nginx/tree/master/deploy/static/provider/baremetal/deploy.yaml

https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.8.0/deploy/static/provider/cloud/deploy.yaml


1. You need to push 2 images to acr for deployment

`az acr import --name <acr_name> --source registry.k8s.io/ingress-nginx/controller:v1.8.0 --image ingress-nginx/controller:v1.8.0`

`az acr import --name <acr_name> --source registry.k8s.io/ingress-nginx/kube-webhook-certgen:v20230407 --image ingress-nginx/kube-webhook-certgen:v20230407`

Assign pull access on acr to aks manage identity

2 Edit the YAML files:
• Edit the deployment.yaml file
# Add Image URL and @sha256 to file
![image](https://github.com/Abhijeetjambaldare14/Nginx-Ingress-Controller-Kubernetes-Manifests/assets/13759950/30456d30-2826-4314-a7fd-59c3a0ecb3ff)


3 Transfer the files to your Kubernetes cluster:
• Transfer the edited YAML files to your Kubernetes cluster

4 Apply the YAML files to your Kubernetes cluster:
• Apply the deploy.yaml file to create the nginx ingress controller deployment, service, and config maps: kubectl apply -f deploy.yaml
![image](https://github.com/Abhijeetjambaldare14/Nginx-Ingress-Controller-Kubernetes-Manifests/assets/13759950/026bba13-626a-4c12-b1ea-86908fe02ab7)


5 Verify the installation:
• Wait for the nginx ingress controller and default backend to be deployed and running: kubectl get pods -n ingress-nginx
• Verify that the ingress controller and default backend services are running: kubectl get svc -n ingress-nginx

# That's it! You should now have a working nginx ingress controller installed on your Kubernetes cluster, even without internet access.

![image](https://github.com/Abhijeetjambaldare14/Nginx-Ingress-Controller-Kubernetes-Manifests/assets/13759950/168c0f9e-eb17-414e-af2b-c78978e51e4c)
