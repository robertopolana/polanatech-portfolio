---
title: "Building Polana AI: Local Infrastructure with Kubernetes and Gemma 3"
date: 2026-01-03T22:00:00+01:00
draft: false
description: "Technical details of a local AI infrastructure deployment using K3s, Docker, and open-source models, with secure global access via Cloudflare Tunnel."
tags: ["MLOps", "Kubernetes", "K3s", "Local AI", "Gemma 3", "Linux", "HomeLab"]
categories: ["Projects", "Infrastructure"]
---

## Context

I developed a local infrastructure dedicated to the technical management of the lifecycle of AI-based applications. The goal of the project is to optimize local hardware resources for the orchestration of containers and LLM models in a scalable and controlled environment.

## Architecture

The **Polana AI** project is based on a robust architecture deployed on dedicated hardware.

* **Hardware:** Intel Core i7 Mini PC with 16GB RAM.
* **OS:** Ubuntu Server (headless).
* **Orchestration:** K3s (Lightweight Kubernetes) for certified container management.
* **AI Engine & UI:** Ollama for model serving and Open WebUI for the user interface.
* **AI Model:** Google Gemma 3 4B.
* **Networking:** Cloudflare Zero Trust Tunnel for secure external access without exposing router ports.

## Build Chronology (January 3, 2026)

### 1. OS Setup
The build started with a clean installation of Ubuntu Server, configuring the system for intensive workloads.

### 2. Orchestration Configuration
After initial testing on Docker, the infrastructure was migrated to **Kubernetes (K3s)** for advanced workload management.
* **Conflict Resolution:** A port conflict between Docker processes and Kubernetes Pods was resolved during migration.
* **Maintenance:** Process auditing (`ps aux`) and system cleanup (`docker system prune`, `ncdu`) were performed to optimize disk space.

### 3. Deploy and Networking
* Initialized the **Gemma 3 4B** model in the Ollama pod's persistent volume via `kubectl exec`.
* Configured the Open WebUI service as `NodePort` for local network access.
* Mapped the **Cloudflare Tunnel** to the internal Service ClusterIP (`http://open-webui:80`) for global access at `ai.polanatech.com`.

## Results and Technical Developments

The infrastructure is currently operational and managed following the Infrastructure as Code paradigm.

Next technical steps include:
* Automating model update cycles via CI/CD pipelines.
* Implementing resource monitoring with Prometheus and Grafana.
* Testing local data integration for the LLM model.