Deploying ArgoCD into a cluster 
=========================================================================================================================
#Ceate namespace
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort"}}'
kubectl -n argocd edit svc argocd-server


#Set current namespace
kubectl config set-context --current --namespace=argocd

#Check if namespace was created
kubectl get namespace

#Create alias 
alias kgn=' kubectl get namespace'
alias g='get'
alias n='namespace'

#Install ArgoCD 
kubectl create -f /tmp/install.yaml -n argocd

#Delete the deployments
kubectl delete -f /tmp/install.yaml

#Password 
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo

username: admin
Passoword: YMRLh3fPFPLqZlKM


Installing ArgoCD CLI 
=========================================================================================================================
curl -sSL -o /usr/local/bin/argocd https://github.com/argoproj/argo-cd/releases/download/v2.4.8/argocd-linux-amd64
chmod +x /usr/local/bin/argocd