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

<img width="1147" height="709" alt="Image" src="https://github.com/user-attachments/assets/90a43f95-9976-4fc8-a181-0d006c2a097d" />

# Task 2: Add a Repository and Search

1. Add the Bitnami repository: helm repo add bitnami https://charts.bitnami.com/bitnami
2. Update: helm repo update
3. Search: helm search repo nginx and helm search repo bitnami

<img width="1920" height="1080" alt="Image" src="https://github.com/user-attachments/assets/a3aadf00-4f7d-4e77-815e-fa65bad4674a" />

<img width="795" height="42" alt="Image" src="https://github.com/user-attachments/assets/f2d0fa78-f849-4619-9dd2-d574794af8f5" />

# Task 3: Install a Chart

1. Deploy nginx: helm install my-nginx bitnami/nginx
2. Check what was created: kubectl get all
3. Inspect the release: helm list, helm status my-nginx, helm get manifest my-nginx

One command replaced writing a Deployment, Service, and ConfigMap by hand.

   <img width="953" height="234" alt="Image" src="https://github.com/user-attachments/assets/8de40975-38e6-41ec-8774-4d98d97a2fe0" />
   <img width="1223" height="733" alt="Image" src="https://github.com/user-attachments/assets/446ff8fe-0f0e-4873-9f26-9b72f1849e9c" />
   <img width="716" height="547" alt="Image" src="https://github.com/user-attachments/assets/f947458a-72ca-4409-9f98-4216b47647bc" />
 
# Task 4: Customize with Values

1. View defaults: helm show values bitnami/nginx
2. Install a custom release with --set replicaCount=3 --set service.type=NodePort
3. Create a custom-values.yaml file with replicaCount, service type, and resource limits
4. Install another release using -f custom-values.yaml
5. Check overrides: helm get values <release-name>

<img width="808" height="269" alt="Image" src="https://github.com/user-attachments/assets/b7c6695d-b361-4ed5-a6a2-bdae0d8c702c" />

<img width="1051" height="360" alt="Image" src="https://github.com/user-attachments/assets/c19f6f50-7379-4b40-a786-3f2adebb2887" />

<img width="883" height="211" alt="Image" src="https://github.com/user-attachments/assets/6b79f268-f619-46eb-bae1-0055ae9fd1c3" />

<img width="672" height="235" alt="Image" src="https://github.com/user-attachments/assets/5e982da9-1b94-4399-ad85-81eecdaa12ce" />

<img width="1010" height="436" alt="Image" src="https://github.com/user-attachments/assets/0430bacc-1ae4-4bab-8bd3-eb569eab539d" />

# Task 5: Upgrade and Rollback

1. Upgrade: helm upgrade my-nginx bitnami/nginx --set replicaCount=5
2. Check history: helm history my-nginx
3. Rollback: helm rollback my-nginx 1
4. Check history again — rollback creates a new revision (3), not overwriting revision 2

Same concept as Deployment rollouts from Day 52, but at the full stack level.

<img width="893" height="237" alt="Image" src="https://github.com/user-attachments/assets/478b8c51-52d6-4781-9d24-40532bdd4703" />

<img width="1144" height="407" alt="Image" src="https://github.com/user-attachments/assets/b7a49532-9282-4ff4-a7f4-35ee128fa1f5" />

