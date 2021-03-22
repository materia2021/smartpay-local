NOTE: this works for docker-desktop only

Important : Make sure you enable kubernetes and your port 80 is open 

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.44.0/deploy/static/provider/cloud/deploy.yaml
kubectl create namespace smartpay
kubectl label nodes docker-desktop node.s3dv.io/currency=<currency low case>
kubectl config set-context --current --namespace=smartpay
docker build -t vnd-smartpay-controller:v1.0 .
docker build -t smartpay-server:v1.0 .
docker build -t smartpay-client:v1.0 .
kubectl apply -k <path to folder kustomization.yaml is located> or you can use . if you are already on the folder
docker run -d -p 5000:5000 --restart=always --name registry registry:2
docker build -t localhost:5000/smartpay-vnd-vsaci:latest --build-arg SCRAPER_NAME=smartpay-scraper-vnd-vsaci .
docker push localhost:5000/smartpay-vnd-vsaci:latest

Connect to our OpenVPN server to have access on our dev DB Service api.

//sender nodejs app
//install yarn first if you don't have npm -g install yarn
//go to sender folder
//modify transaction details inside index.js and run the ff commands
yarn
node index.js

optional: 
dashoard installation 

kubectl create -f https://raw.githubusercontent.com/kubernetes/dashboard/master/aio/deploy/recommended/kubernetes-dashboard.yaml
kubectl create serviceaccount dashboard-admin-sa
kubectl create clusterrolebinding dashboard-admin-sa --clusterrole=cluster-admin --serviceaccount=default:dashboard-admin-sa
kubectl get secrets
//copy the secret name should be something like dashboard-admin-sa-token-*
kubectl describe secret <secret name>
//copy the token
kubectl proxy
http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/
//login using token

argo installation

kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
kubectl port-forward svc/argocd-server -n argocd 8080:443
http://localhost:8080
kubectl --namespace argocd get secret argocd-secret -o json | jq '.data | map_values(@base64d)'

ref https://kubernetes.io/docs/reference/kubectl/cheatsheet/