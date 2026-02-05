# Legacy Application Migration to Kubernetes (DevOps Case Study)

## Overview

This repository documents a real-world DevOps case study where a legacy application
(originally running on **Windows Server 2008 with IIS**) was successfully migrated
to a **containerized microservices architecture on Kubernetes**.

The goal was to modernize deployment, improve reliability, and enable automated CI/CD
without modifying the original business logic.

> ⚠️ All names, domains, IPs, credentials, and identifiers have been anonymized.

---

## Initial Situation

- Legacy application running on:
  - Windows Server 2008
  - IIS
  - Very old GeneXus version (non-upgradable)
- Security incompatibilities with modern TLS and auth standards
- Manual deployments
- No CI/CD
- High operational risk

Decision: **Rebuild application + redesign infrastructure**

---

## Target Architecture

- Backend:
  - Java 21 + Spring Boot
  - Containerized with Docker
- Frontend:
  - Node.js + Vue
  - Nginx running as non-root
- Platform:
  - Kubernetes
  - GitLab CI/CD
  - Argo CD (GitOps)
- Registry:
  - Private container registry
- Ingress:
  - Nginx Ingress Controller
- Authentication:
  - Reverse proxy integration with external identity API (LDAP-backed)

---

## CI/CD Design

### Backend Pipeline

- Maven build
- Artifact generation
- Cross-project pipeline trigger
- Docker image build using Kaniko
- GitOps deployment via Argo CD

📄 See: `ci-cd/backend-gitlab-ci.yml`

### Frontend Pipeline

- Node.js build
- Artifact packaging
- Nginx-based runtime image
- Non-root container hardening
- Same GitOps flow as backend

📄 See: `ci-cd/frontend-gitlab-ci.yml`

---

## Infrastructure Pipeline

A centralized infrastructure repository handles:

- Artifact download
- Image building (Kaniko)
- Image tagging per environment
- Kubernetes manifest updates
- Automatic Argo CD sync

📄 See: `ci-cd/infra-gitlab-ci.yml`

---

## Kubernetes Implementation

- Namespaced deployments per environment
- ConfigMaps for configuration
- Readiness & liveness probes
- Resource requests/limits
- SecurityContext with non-root containers
- Ingress routing frontend and backend traffic

📂 See: `kubernetes/`

---

## Authentication Challenge & Solution

The frontend required authentication via an **external identity API**
instead of local Nginx auth.

Solution:
- Implemented Nginx reverse proxy
- Proper header forwarding
- Resolved HTTP 405 and auth flow issues

📄 See: `docker/frontend/default.conf`

---

## GitOps with Argo CD

- Declarative deployments
- Automated sync
- Self-healing enabled
- Environment-based separation

📄 See: `argo-cd/application.yaml`

---

## Key DevOps Skills Demonstrated

- Legacy system modernization
- CI/CD pipeline design
- Cross-repository orchestration
- Secure containerization
- Kubernetes production patterns
- GitOps with Argo CD
- Troubleshooting complex auth and networking issues

---

## Author

**Senior DevOps Engineer**  
15+ years in infrastructure evolution  
Focus on automation, reliability, and modernization
