# ArgoCD install

**Installation:**

```bash
# Delete any existing minikube instance
minikube delete

# Start minikube with 2 CPUs and 7.9 GB of memory
minikube start --cpus=2 --memory=7900MB

# Add the Argo Helm repository
helm repo add argo https://argoproj.github.io/argo-helm

# Update the Helm repositories
helm repo update

# Create the Argo CD namespace
kubectl create namespace argocd

# Change to the Argo CD directory
cd /workspaces/openshift-argocd/6_Symbols/2_ArgoCd

# Install Argo CD
```bash
# Install Argo CD with custom values and enable debugging
helm install argocd argo/argo-cd --namespace argocd -f values.yaml --debug 

```

**Testing:**
# Install Argo CD with custom values and enable debugging

helm install argocd argo/argo-cd --namespace argocd -f values.yaml --debug --dry-run
```bash
# Get a list of pods in the Argo CD namespace
kubectl get pods -n argocd

# Get the initial admin password
kubectl get secret argocd-secret -n argocd -o jsonpath="{.data.admin\.password}" | base64 -d
```

**Optional:**

```bash
# Get a list of nodes
kubectl get nodes

# Upgrade Argo CD
helm upgrade argocd argo/argo-cd --namespace argocd -f values.yaml

# Get a list of pods in the Argo CD namespace
kubectl get pods -n argocd
```

**Accessing the UI:**

```bash
# Forward the Argo CD server port to your local machine
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

**Logging in to Argo CD:**

```bash
# Get the initial admin password
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

**Customizing Argo CD:**

```bash
# Install Argo CD with custom values
helm install argocd argo/argo-cd --namespace argocd -f values.yaml
```

---
prompt:
- only leave the commands
- Use the markdown structure 
- Use emojis
- use ascii
