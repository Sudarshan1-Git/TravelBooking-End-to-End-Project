# ✈️ TravelBooking End-to-End DevSecOps Project

A production-style **microservices-based Travel Booking application** used to build a complete End-to-End **DevSecOps project from scratch**.

The goal of this project is to implement containerization, CI/CD, security scanning, Infrastructure as Code, Kubernetes, GitOps, monitoring, centralized logging, and alerting using modern DevOps tools and AWS.

> 🚧 **Project Status:** In Progress  
>
> The application source code is available. The DevOps infrastructure and pipelines are being implemented step by step from scratch.

---

## 📌 Project Objectives

This project will demonstrate:

- Microservices deployment
- Docker containerization
- CI using GitHub Actions
- Code quality analysis using SonarQube
- Vulnerability scanning using Trivy
- AWS infrastructure provisioning using Terraform
- Container image storage using Amazon ECR
- Kubernetes deployment using Amazon EKS
- Kubernetes traffic management using Ingress
- GitOps Continuous Deployment using ArgoCD
- Metrics collection using Prometheus
- Monitoring dashboards using Grafana
- Centralized logging using Loki
- Log collection using Grafana Alloy
- Alerting using Prometheus Alertmanager

---

# 🏗️ Application Architecture

The TravelBooking application follows a **microservices architecture**.

```text
                        User
                         │
                         ▼
                  React Frontend
                         │
            ┌────────────┼────────────┐
            │            │            │
            ▼            ▼            ▼
      User Service   Search Service  Booking Service
          :3001          :3002           :3003
                                           │
                                  ┌────────┴────────┐
                                  │                 │
                                  ▼                 ▼
                           Payment Service   Notification Service
                               :3004               :3005

                                  │
                         ┌────────┴────────┐
                         ▼                 ▼
                     PostgreSQL           Redis
```

---

# 🧩 Microservices

The backend is written in **Go** and is divided into independent microservices.

| Service | Purpose | Port |
|---|---|---:|
| User Service | Authentication and user management | 3001 |
| Search Service | Flight and hotel search | 3002 |
| Booking Service | Travel booking management | 3003 |
| Payment Service | Payment processing | 3004 |
| Notification Service | Application notifications | 3005 |

The frontend is developed using **React**.

---

# 🛠️ Technology Stack

## Application

| Technology | Purpose |
|---|---|
| React | Frontend |
| Go | Backend microservices |
| PostgreSQL | Relational database |
| Redis | Caching |

## DevSecOps

| Technology | Purpose |
|---|---|
| Git | Version Control |
| GitHub | Source Code Management |
| Docker | Containerization |
| Docker Compose | Local multi-container deployment |
| GitHub Actions | Continuous Integration |
| SonarQube | Static code analysis / Code quality |
| Trivy | Vulnerability scanning |
| Amazon ECR | Docker image registry |
| Terraform | Infrastructure as Code |
| AWS | Cloud platform |
| Amazon EKS | Managed Kubernetes |
| Kubernetes | Container orchestration |
| Ingress | Application traffic routing |
| ArgoCD | GitOps Continuous Deployment |
| Prometheus | Metrics collection |
| Grafana | Monitoring dashboards |
| Loki | Centralized logging |
| Grafana Alloy | Log collection |
| Alertmanager | Alert management and notification |

---

# 🔄 CI/CD Architecture

The CI/CD pipeline will follow a **CI + GitOps CD** approach.

```text
Developer
    │
    │ git push
    ▼
GitHub
    │
    ▼
GitHub Actions
    │
    ├── Build / Test
    │
    ├── SonarQube Analysis
    │
    ├── Trivy Filesystem Scan
    │
    ├── Docker Build
    │
    └── Trivy Image Scan
    │
    ▼
Amazon ECR
    │
    ▼
Update Kubernetes Image Tag
    │
    ▼
Git Repository
    │
    ▼
ArgoCD
    │
    ▼
Amazon EKS
    │
    ▼
Kubernetes Deployment
```

---

# 🔁 Continuous Integration

**GitHub Actions** will be responsible for Continuous Integration.

The planned CI pipeline includes:

```text
Code Push
   ↓
Checkout
   ↓
Install Dependencies
   ↓
Build / Test
   ↓
SonarQube Analysis
   ↓
Trivy Filesystem Scan
   ↓
Docker Image Build
   ↓
Trivy Image Scan
   ↓
Push Image → Amazon ECR
```

GitHub Actions will **not directly deploy the application to Kubernetes**.

Deployment will be handled by ArgoCD using GitOps.

---

# 🚀 Continuous Deployment with ArgoCD

ArgoCD will continuously monitor the Kubernetes configuration stored in Git.

```text
Git Repository
      │
      ▼
    ArgoCD
      │
      │ Detect configuration change
      ▼
   Amazon EKS
      │
      ▼
Kubernetes Resources
```

This separates:

**CI**

```text
GitHub Actions
```

from:

**CD**

```text
ArgoCD
```

---

# ☁️ AWS Infrastructure

AWS infrastructure will be provisioned using **Terraform**.

The planned infrastructure includes:

```text
AWS
│
├── VPC
│   ├── Public Subnets
│   ├── Private Subnets
│   ├── Route Tables
│   ├── Internet Gateway
│   └── NAT Gateway (where required)
│
├── Amazon ECR
│   ├── frontend
│   ├── user-service
│   ├── search-service
│   ├── booking-service
│   ├── payment-service
│   └── notification-service
│
└── Amazon EKS
    ├── EKS Cluster
    └── Worker Nodes
```

Terraform will allow the infrastructure to be:

- Version controlled
- Reproducible
- Automated
- Consistent across environments

---

# ☸️ Kubernetes Architecture

The application will eventually run on **Amazon EKS**.

Each microservice will have its own Kubernetes resources.

```text
Internet
    │
    ▼
AWS Load Balancer / Ingress
    │
    ▼
Frontend Service
    │
    ▼
Frontend Pods
    │
    ├──────────────┬──────────────┐
    ▼              ▼              ▼
 User           Search         Booking
 Service        Service        Service
    │              │              │
    ▼              ▼              ▼
  Pods           Pods           Pods
                                  │
                          ┌───────┴───────┐
                          ▼               ▼
                       Payment       Notification
                       Service          Service
                          │               │
                          ▼               ▼
                         Pods            Pods
```

Kubernetes resources will include:

- Namespaces
- Deployments
- Services
- ConfigMaps
- Secrets
- Ingress
- Resource requests and limits
- Health checks

---

# 🔐 DevSecOps Security

Security checks will be integrated into the CI pipeline.

## SonarQube

SonarQube will be used for:

- Static code analysis
- Code quality checks
- Bug detection
- Code smell detection
- Maintainability analysis

## Trivy

Trivy will be used for:

- Filesystem vulnerability scanning
- Dependency scanning
- Docker image vulnerability scanning
- Container security checks

The security pipeline will follow:

```text
Source Code
    │
    ├── SonarQube
    │
    └── Trivy Filesystem Scan
            │
            ▼
       Docker Build
            │
            ▼
       Trivy Image Scan
            │
            ▼
         Amazon ECR
```

---

# 📊 Monitoring

The Kubernetes environment and application will be monitored using:

- Prometheus
- Grafana
- kube-state-metrics
- Node Exporter

```text
Application / Kubernetes
          │
          ▼
      Prometheus
          │
          ▼
       Grafana
          │
          ▼
      Dashboards
```

Metrics will include:

- CPU usage
- Memory usage
- Pod health
- Node health
- Deployment replicas
- Application availability
- HTTP request metrics
- Response latency

---

# 📜 Centralized Logging

Application and Kubernetes logs will be centralized using:

```text
Application Pods
       │
       ▼
 Container Logs
       │
       ▼
 Grafana Alloy
       │
       ▼
      Loki
       │
       ▼
    Grafana
```

This will allow logs from different microservices to be searched and analyzed from a single interface.

---

# 🚨 Alerting

Prometheus alerting rules and **Alertmanager** will be used for infrastructure and application alerts.

Planned alerts include:

- High CPU utilization
- High memory utilization
- Pod unavailable
- Pod restart/crash
- Node unavailable
- Deployment replicas unavailable
- Application endpoint unavailable
- High HTTP 5xx error rate
- High application latency
- Storage/resource issues

Alert flow:

```text
Application / EKS
       │
       ▼
   Prometheus
       │
       ▼
   Alert Rules
       │
       ▼
  Alertmanager
       │
       ├── Email
       └── Other notification channels
```

Alerts will be tested by deliberately creating failures and verifying that Prometheus and Alertmanager detect and report them.

---

# 📁 Project Structure

```text
TravelBooking-End-to-End-Project/
│
├── frontend/
│   ├── public/
│   ├── src/
│   └── package.json
│
├── user-service/
│   ├── internal/
│   ├── go.mod
│   └── main.go
│
├── search-service/
│   ├── internal/
│   ├── go.mod
│   └── main.go
│
├── booking-service/
│   ├── internal/
│   ├── go.mod
│   └── main.go
│
├── payment-service/
│   ├── internal/
│   ├── go.mod
│   └── main.go
│
├── notification-service/
│   ├── internal/
│   ├── go.mod
│   └── main.go
│
├── postgres/
│   └── init.sql
│
├── .gitignore
└── README.md
```

Additional DevOps directories will be added as the project progresses.

The final structure is expected to include:

```text
├── .github/
│   └── workflows/
│
├── terraform/
│
├── kubernetes/
│
├── argocd/
│
└── monitoring/
```

---

# 🗺️ Implementation Roadmap

### Phase 1 — Application

- [x] Application source code
- [ ] Understand microservices architecture
- [ ] Configure environment variables
- [ ] Configure PostgreSQL
- [ ] Configure Redis
- [ ] Run backend microservices locally
- [ ] Run frontend locally
- [ ] Test complete application

### Phase 2 — Containerization

- [ ] Create Dockerfile for frontend
- [ ] Create Dockerfiles for Go microservices
- [ ] Implement multi-stage builds
- [ ] Create `.dockerignore`
- [ ] Build Docker images
- [ ] Create Docker Compose configuration
- [ ] Run complete application using Docker Compose

### Phase 3 — CI & Security

- [ ] Create GitHub Actions workflow
- [ ] Configure application build/test
- [ ] Integrate SonarQube
- [ ] Integrate Trivy filesystem scanning
- [ ] Build Docker images automatically
- [ ] Scan Docker images using Trivy
- [ ] Push images to Amazon ECR

### Phase 4 — Infrastructure

- [ ] Configure Terraform
- [ ] Configure remote Terraform state
- [ ] Create AWS VPC
- [ ] Create subnets
- [ ] Create networking resources
- [ ] Create Amazon ECR repositories
- [ ] Create Amazon EKS cluster
- [ ] Create EKS worker nodes

### Phase 5 — Kubernetes

- [ ] Create Namespace
- [ ] Create ConfigMaps
- [ ] Create Secrets
- [ ] Create Deployments
- [ ] Create Services
- [ ] Configure health checks
- [ ] Configure resource requests/limits
- [ ] Configure Ingress
- [ ] Deploy application to EKS

### Phase 6 — GitOps

- [ ] Install ArgoCD
- [ ] Connect Git repository
- [ ] Create ArgoCD Application
- [ ] Configure automatic synchronization
- [ ] Test GitOps deployment

### Phase 7 — Monitoring & Logging

- [ ] Install Prometheus
- [ ] Install Grafana
- [ ] Configure Kubernetes metrics
- [ ] Create Grafana dashboards
- [ ] Install Loki
- [ ] Configure Grafana Alloy
- [ ] Centralize application logs

### Phase 8 — Alerting

- [ ] Configure Prometheus alert rules
- [ ] Install/configure Alertmanager
- [ ] Configure notification channel
- [ ] Configure CPU alert
- [ ] Configure memory alert
- [ ] Configure pod health alert
- [ ] Configure application availability alert
- [ ] Test alert generation

---

# 🎯 Final DevSecOps Workflow

```text
                         Developer
                             │
                          Git Push
                             │
                             ▼
                           GitHub
                             │
                             ▼
                      GitHub Actions
                             │
              ┌──────────────┼──────────────┐
              ▼              ▼              ▼
            Build        SonarQube        Trivy
              │              │              │
              └──────────────┼──────────────┘
                             ▼
                       Docker Build
                             │
                             ▼
                       Trivy Scan
                             │
                             ▼
                         Amazon ECR
                             │
                             ▼
                       GitOps Repository
                             │
                             ▼
                           ArgoCD
                             │
                             ▼
                         Amazon EKS
                             │
                             ▼
                         Kubernetes
                             │
                   ┌─────────┴─────────┐
                   ▼                   ▼
              Application         Observability
                                      │
                         ┌────────────┼────────────┐
                         ▼            ▼            ▼
                    Prometheus      Loki        Grafana
                         │
                         ▼
                    Alertmanager
                         │
                         ▼
                    Notifications
```

---

# 📚 Key Learning Outcomes

By completing this project, the following concepts will be demonstrated:

- Microservices architecture
- Docker containerization
- Multi-stage Docker builds
- CI/CD pipeline design
- DevSecOps security integration
- Infrastructure as Code
- AWS networking
- Amazon ECR
- Amazon EKS
- Kubernetes deployments
- Kubernetes networking
- GitOps
- Infrastructure monitoring
- Application monitoring
- Centralized logging
- Alert management
- Production-style troubleshooting

---

## 👤 Author

**Sudarshan**

---

## 📌 Status

🚧 **Currently under active development**

The README will be updated as each phase of the project is implemented and tested.
