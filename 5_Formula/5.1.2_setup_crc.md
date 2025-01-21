Here is your GitHub Markdown formatted blog post:

---

# Streamlining Your CI/CD Workflow with OpenShift and GitOps

OpenShift clusters can streamline your CI/CD workflow by integrating GitOps practices. This blog post will guide you through setting up ArgoCD, configuring Helm, and deploying an application on a CRC OpenShift cluster. We will cover the following steps:

1. **Setting Up CRC (CodeReady Containers) OpenShift Cluster**
2. **Installing ArgoCD on OpenShift**
3. **Configuring Helm on OpenShift**
4. **Deploying an Application using Helm and ArgoCD**

Let's dive in!

## 1. Setting Up CRC (CodeReady Containers) OpenShift Cluster

CodeReady Containers (CRC) provides a minimal OpenShift 4 cluster, making it easy to test and develop on OpenShift locally. Follow these steps to get your CRC OpenShift cluster up and running:

### Step 1: Install CRC

Download and install CRC from the official Red Hat website. Make sure your system meets the minimum requirements. Once installed, start the CRC cluster:

```bash
crc setup
crc start
```

During the `crc start` command, you’ll be prompted to provide a pull secret. You can obtain this secret from the Red Hat OpenShift Cluster Manager.

### Step 2: Log in to OpenShift

After starting the CRC, log in to your OpenShift cluster using the credentials provided:

```bash
oc login -u kubeadmin -p <password> https://api.crc.testing:6443
```

Replace `<password>` with the one displayed at the end of the `crc start` process.

## 2. Installing ArgoCD on OpenShift

To deploy Argo CD using Helm, you need to follow several steps to ensure a smooth installation and configuration of the tool. Helm is a package manager for Kubernetes that allows you to define, install, and upgrade complex Kubernetes applications. Argo CD is a popular continuous delivery tool for Kubernetes, which makes it easy to implement GitOps practices by managing application deployments in a declarative manner.

### Step 1: Install Helm

If you haven't installed Helm yet, you can install it by following the instructions on the [official Helm website](https://helm.sh/docs/intro/install/).

### Step 2: Add the Argo CD Helm repository

First, add the Argo CD Helm repository to your Helm client:

```bash
helm repo add argo https://argoproj.github.io/argo-helm
helm repo update
```

### Step 3: Create a Namespace for Argo CD

It's a good practice to deploy Argo CD in its own namespace. Create a namespace for Argo CD:

```bash
oc create namespace argocd
```

### Step 4: Install Argo CD using Helm

Now, use Helm to install Argo CD into the namespace you just created. You can use the default values or customize them as needed.

To install Argo CD with the default settings, run:

```bash
helm install argocd argo/argo-cd --namespace argocd
```

### Step 5: Check the Installation

To verify that Argo CD has been installed correctly, you can check the pods running in the `argocd` namespace:

```bash
oc get pods -n argocd
```

You should see several pods, including `argocd-server`, `argocd-repo-server`, `argocd-redis`, and others.

### Step 6: Access the Argo CD UI

By default, Argo CD's API server is not exposed via a LoadBalancer or Ingress. You can access it using `kubectl port-forward`:

```bash
oc port-forward svc/argocd-server -n argocd 8080:443
```

Now you can open your web browser and go to `https://localhost:8080` to access the Argo CD web UI.

### Step 7: Login to Argo CD

The initial password for the admin user is auto-generated and stored in a Kubernetes secret. To get this password, run:

```bash
oc -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

or for PowerShell users:

```powershell
oc -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | ForEach-Object { [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($_)) }
```

Use the username `admin` and the password you retrieved to log in to the Argo CD UI.

### Step 8: (Optional) Customize Argo CD Installation

If you need to customize your Argo CD installation, you can create a `values.yaml` file and specify your custom configurations there. Here’s an example command to install Argo CD with custom values:

Create a `values.yaml` file:

```yaml
server:
  service:
    type: LoadBalancer
```

Install Argo CD using the custom `values.yaml`:

```bash
helm install argocd argo/argo-cd --namespace argocd -f values.yaml
```

This will install Argo CD with the specified customizations.

## Summary

You've now deployed Argo CD on your Kubernetes cluster using Helm! You can customize further based on your requirements, such as enabling SSL, configuring authentication, or setting up Argo CD projects and applications.

If you have any further questions or need more customization details, feel free to ask!

---

This format should work well for a GitHub Markdown document, and it includes all the necessary details for your CI/CD setup using OpenShift, ArgoCD, and Helm.