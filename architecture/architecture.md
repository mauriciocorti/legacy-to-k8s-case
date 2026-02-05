
Architecture Overview
Context and Motivation

RegistroVisitas was a legacy application responsible for a single but critical task: registering every visitor arriving at the central building.

The original system was:

Developed with GeneXus

Running on IIS

Hosted on Windows Server 2008

Over time, this server became a significant security risk due to its obsolete operating system and limited support. Decommissioning this Windows Server 2008 instance became a clear and urgent objective for the infrastructure and security teams.

Modernization Strategy

Instead of attempting an in-place upgrade, the development team decided to rebuild the application using a modern, cloud-native stack:

Backend: Java with Spring Boot

Frontend: Node.js with Vue.js

Database: PostgreSQL (new instance)

Authentication: External authentication API (consumed by the backend)

This approach allowed the team to:

Eliminate legacy dependencies

Improve maintainability and scalability

Align with containerization and Kubernetes standards

Target Infrastructure Architecture

The new RegistroVisitas platform is deployed on a Kubernetes-based infrastructure, following modern DevOps and GitOps principles.

High-Level Components

Frontend Application

Vue.js application served via Node.js container

Exposed externally through Kubernetes Ingress

Backend Application

Spring Boot REST API

Handles business logic and integration with authentication API

Database Layer

PostgreSQL database

Provisioned separately from the application lifecycle

Authentication Service

External API

Consumed securely by the backend

Deployment Environments
Integration Environment

All components are initially deployed in an Integration environment, where:

Functional teams validate business flows

The legacy system remains fully operational

No production traffic is affected

This parallel-run strategy ensures:

Safe validation

Controlled risk

Zero disruption to current operations

Production Environment

Once functional validation is approved:

The same Kubernetes manifests are promoted to Production

Traffic is switched to the new platform

The legacy Windows Server 2008 hosting RegistroVisitas is decommissioned and removed

This final step represents the successful completion of the migration and the elimination of a long-standing security liability.

DevOps and Delivery Model

Applications are containerized using Docker

CI pipelines are implemented with GitLab CI

Kubernetes manifests are managed declaratively

Argo CD is used to synchronize and deploy applications following a GitOps approach

Key Outcomes

Complete shutdown of a vulnerable Windows Server 2008 system

Adoption of a modern, scalable, and secure architecture

Clear separation between environments

Repeatable and auditable deployment process

From a personal and professional standpoint, decommissioning this legacy server was a major milestone and a long-standing goal finally achieved.