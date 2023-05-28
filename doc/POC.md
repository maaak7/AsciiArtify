# ArgoCD k3d Setup

## Precondition
You must have [k3d](https://k3d.io/v5.5.1/#installation) and [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/) installed locally

## Setup
1. Create k3d cluster for argo - `k3d cluster create argo`
2. Check everything works properly - `kubectl cluster-info` | `kubectl get all -A`
3. Create namespace - `kubectl create namespace argocd`
4. Install ArgoCD on Kubernetes cluster - `kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml`
5. Check details by `kubectl get all -n argocd` | `kubectl  get po -n argocd -w`
6. Get access to ArgoCD UI by entering command `kubectl port-forward svc/argocd-server -n argocd 8080:443&`
7. Now you can open your ArgoCD UI in your browser - `127.0.0.1:8080`
8. Get your `admin` password with command - `kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo`

That's it. Now you can [create your apps via UI](https://argo-cd.readthedocs.io/en/stable/getting_started/#creating-apps-via-ui)!