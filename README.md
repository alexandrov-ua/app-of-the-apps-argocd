# app-of-the-apps-argocd

To setup it locally (kubernetes.docker.internal)

1. Install ingress
```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.0.4/deploy/static/provider/cloud/deploy.yaml
kubectl patch ingressclass nginx -p '{"metadata": {"annotations":{"ingressclass.kubernetes.io/is-default-class":"true"}}}'
```
https://github.com/entei-11/kubernetes.docker.internal/blob/main/init-ingress-nginx.sh

2. Install ArgoCD (https://argo-cd.readthedocs.io/en/stable/getting_started/)
```
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

```
2.1. Forward port to ArgoCD 
```
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
2.2. Get the password
```
argocd admin initial-password -n argocd
```

3. Apply initial app

```
kubectl apply -f argocd-app.yaml
```
