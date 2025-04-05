# 🛠️ CI/CD Microservices Project with Kubernetes

This project demonstrates a **real-world end-to-end CI/CD pipeline** setup using a **Node.js/Express backend (`user-service`, `task-service`)**, a **React frontend**, and a **Kubernetes-based deployment** workflow. It showcases automation, infrastructure-as-code, debugging, and deployment best practices in a microservices architecture.

---

## 📦 Tech Stack

- **Frontend**: React
- **Backend**: Node.js (Express)
- **Containerization**: Docker
- **CI/CD**: GitHub Actions
- **Orchestration**: Kubernetes (k8s)
- **IaC**: Terraform (for cluster setup)
- **Cloud Platform**: AWS (EKS assumed)
- **Namespace**: `workshop`

---

## 🚀 Features

- Microservices-based app (User & Task Services)
- React UI to interact with backend APIs
- Dockerized for consistency across environments
- GitHub Actions for automated build, lint, test & deploy
- Kubernetes deployment with isolated namespace
- Helm support for future extension
- Troubleshooting & recovery strategies included

---

## 🧱 Project Structure

ci-cd-microservices-app/ ├── backend/ │ ├── user-service/ │ │ ├── Dockerfile │ │ └── deployment.yaml │ ├── task-service/ │ │ ├── Dockerfile │ │ └── deployment.yaml ├── frontend/ │ ├── Dockerfile │ └── deployment.yaml ├── k8s/ │ ├── namespace.yaml │ ├── ingress.yaml │ └── service.yaml ├── .github/workflows/ │ ├── ci.yaml │ └── cd.yaml

---

## 🐳 Docker Setup

Each service has its own `Dockerfile`.

### Example: `user-service/Dockerfile`

```Dockerfile
FROM node:18-alpine
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 3001
CMD ["node", "index.js"]
Push your Docker images to DockerHub:
docker build -t yourdockerhubusername/user-service .
docker push yourdockerhubusername/user-service
Repeat for task-service and frontend.

☸️ Kubernetes Setup
kubectl create ns workshop
Apply Deployments & Services
kubectl apply -f k8s/ -n workshop
Each deployment.yaml includes:

containerPort: Internal port exposed by the container

targetPort: Port the service forwards to inside the pod

port: Port exposed by the Kubernetes service

✅ Ensure consistency in containerPort/targetPort across your YAML files.

⚠️ Troubleshooting
❌ ImagePullBackOff
Reason: Wrong image name or private repo.

Fix:

Ensure Docker image is public or set up imagePullSecrets.

Confirm image exists: docker pull yourdockerhubusername/frontend-app:latest

Correct YAML:
image: yourdockerhubusername/frontend-app:latest

❌ CrashLoopBackOff
Reason: The container crashes after starting.

Debug:

bash
Copy
Edit
kubectl logs -n workshop pod-name
Fix:

Check missing environment variables.

Validate CMD or ENTRYPOINT in Dockerfile.

Confirm PORT is set and matches the exposed port.

✅ Example Commands Used
bash
Copy
Edit
kubectl config set-context --current --namespace=workshop
kubectl get pods -n workshop
kubectl describe pod <pod-name> -n workshop
kubectl logs <pod-name> -n workshop

🧪 CI/CD (GitHub Actions)
ci.yaml (Build & Lint)
Triggers on push to main

Runs npm install, lint, unit tests, and builds Docker images

cd.yaml (Deploy to k8s)
Pushes Docker images

Applies k8s manifests using kubectl

🔍 Lessons Learned
How to debug ImagePullBackOff and CrashLoopBackOff

Importance of correct container ports and image references

Deploying multi-service apps using Kubernetes

Handling CI/CD failures and rollout strategies

Use of namespaces to isolate environments in Kubernetes


👩‍💻 Author
Felix Oppong – Cloud & DevOps Enthusiast
GitHub • Portfolio • LinkedIn

📌 Final Notes
This project was developed as part of a personal challenge to master DevOps tools and cloud-native microservice deployments. All errors encountered were treated as learning opportunities, documented, and resolved hands-on.

