# devops-k8s-migration-case-

devops-k8s-migration-case/
├── README.md
├── architecture/
│   └── architecture.md
├── ci-cd/
│   ├── backend-gitlab-ci.yml
│   ├── frontend-gitlab-ci.yml
│   └── infra-gitlab-ci.yml
├── docker/
│   ├── backend/
│   │   └── Dockerfile
│   └── frontend/
│       ├── Dockerfile
│       └── default.conf
├── kubernetes/
│   ├── backend/
│   │   ├── configmap.yaml
│   │   ├── deployment.yaml
│   │   ├── service.yaml
│   │   └── ingress.yaml
│   └── frontend/
│       ├── deployment.yaml
│       ├── service.yaml
│       └── ingress.yaml
├── argo-cd/
│   └── application.yaml
└── SECURITY.md
