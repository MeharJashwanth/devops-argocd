# Steps to install ArgoCD on Minikube
## Installation Steps:
1. Start Minikube: Launch your Minikube cluster using a compatible driver. The docker driver is a common choice.

      ### minikube start --driver=docker
2. Create a Namespace: It's a best practice to install Argo CD in its own dedicated namespace.

      ### kubectl create namespace argocd
3. Apply Argo CD Manifests: Use kubectl to apply the official installation manifest from the Argo CD GitHub repository.

      ### kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
4. Access the Argo CD UI: By default, the Argo CD API server isn't exposed externally. You can use port forwarding to access the web UI on your local machine.
   
      ### kubectl port-forward svc/argocd-server -n argocd 8080:443
5. Retrieve Initial Password: The default admin password is auto-generated and stored in a Kubernetes secret. Retrieve it using kubectl.

      ### kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
