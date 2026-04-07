# Day-59-Helm-Kubernetes-Package-Manager

# Task

Over the past eight days you have written Deployments, Services, ConfigMaps, Secrets, PVCs, and more — all as individual YAML files. For a real application you might have dozens of these. Helm is the package manager for Kubernetes, like apt for Ubuntu. Today you install charts, customize them, and create your own.

# Expected Output

- Helm installed and a chart deployed from Bitnami
- A release customized, upgraded, and rolled back
- A custom chart created and installed
- A markdown file: day-59-helm.md

# Challenge Tasks

# Task 1: Install Helm

1. Install Helm (brew, curl script, or chocolatey depending on your OS)
2. Verify with helm version and helm env
   
Three core concepts:

- Chart — a package of Kubernetes manifest templates
- Release — a specific installation of a chart in your cluster
- Repository — a collection of charts (like a package repo)

# Task 2: Add a Repository and Search

1. Add the Bitnami repository: helm repo add bitnami https://charts.bitnami.com/bitnami
2. Update: helm repo update
3. Search: helm search repo nginx and helm search repo bitnami

# Task 3: Install a Chart

1. Deploy nginx: helm install my-nginx bitnami/nginx
2. Check what was created: kubectl get all
3. Inspect the release: helm list, helm status my-nginx, helm get manifest my-nginx

One command replaced writing a Deployment, Service, and ConfigMap by hand.

# Task 4: Customize with Values

1. View defaults: helm show values bitnami/nginx
2. Install a custom release with --set replicaCount=3 --set service.type=NodePort
3. Create a custom-values.yaml file with replicaCount, service type, and resource limits
4. Install another release using -f custom-values.yaml
5. Check overrides: helm get values <release-name>

# Task 5: Upgrade and Rollback

1. Upgrade: helm upgrade my-nginx bitnami/nginx --set replicaCount=5
2. Check history: helm history my-nginx
3. Rollback: helm rollback my-nginx 1
4. Check history again — rollback creates a new revision (3), not overwriting revision 2

Same concept as Deployment rollouts from Day 52, but at the full stack level.
