# ArgoCD install
- minikube delete
- minikube start --cpus=2 --memory=7900MB
--------------- one time ---------------------------------
- helm repo add argo https://argoproj.github.io/argo-helm
- helm repo update
--------------------------------------------------------------

- kubectl create namespace argocd
- cd /workspaces/openshift-argocd/6_Symbols/2_ArgoCd
- helm install argocd argo/argo-cd --namespace argocd -f values.yaml

--------------------- test ------------------------------------
- kubectl get pods -n argocd
- kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
---------------------------------------------------------------
-------------------- optional ------------------------------
- kubectl get nodes
- helm upgrade argocd argo/argo-cd --namespace argocd -f values.yaml
- kubectl get pods -n argocd
------------------------------------------------------------
```
6. Access the Argo CD UI:
```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
7. Login to Argo CD:
```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```
8. (Optional) Customize Argo CD Installation
```bash
helm install argocd argo/argo-cd --namespace argocd -f values.yaml
```

---
prompt:
- only leave the commands
- Use the markdown structure 
- Use emojis
- use ascii
