---
title: "Building Polana AI: From Zero to Local MLOps with Kubernetes and Gemma 3"
date: 2026-01-03T22:00:00+01:00
draft: false
description: "How I transformed a Mini PC into a production-grade AI infrastructure using K3s, Docker, and open-source models, with secure global access via Cloudflare Tunnel."
tags: ["MLOps", "Kubernetes", "K3s", "Local AI", "Gemma 3", "Linux", "HomeLab"]
categories: ["Projects", "Infrastructure"]
---

## The Context

On my path as an **IT Specialist** specializing toward **MLOps** roles, I decided to build a local infrastructure to manage the entire lifecycle of an AI-based application. The goal was to move from theory to practice, orchestrating containers and LLM models in a controlled yet scalable environment.

## The Architecture

The **Polana AI** project is more than just a software installation; it is a full-stack architecture built on commodity hardware.

* **Hardware:** Intel Core i7 Mini PC with 16GB RAM.
* **OS:** Ubuntu Server (headless) to maximize resource allocation.
* **Orchestration:** K3s (Lightweight Kubernetes) for efficient and certified container management.
* **AI Engine & UI:** Ollama for model serving and Open WebUI for the user interface.
* **AI Model:** Google Gemma 3 4B (the 2026 standard for efficiency).
* **Networking:** Cloudflare Zero Trust Tunnel for secure external access without port forwarding.

## Build Timeline (January 3, 2026)

### 1. Bare Metal Installation
The process began with a clean install of Ubuntu Server via USB, preparing the hardware for its new role as an AI node.

### 2. Transitioning to Orchestration
I initially tested the deployment using standard Docker. However, to align with MLOps best practices, I quickly migrated to **Kubernetes (K3s)**.
* **Technical Challenge:** During the migration, a port conflict occurred between legacy Docker processes and the new Kubernetes Pods.
* **Resolution:** I performed a process audit using `ps aux` and `docker ps`, terminated old containers, and cleaned the system with `docker system prune` and `ncdu` to reclaim disk space, clearing the path for K3s.

### 3. Deployment and Configuration
Once the K3s cluster was stabilized:
1.  I pulled the **Gemma 3 4B** model directly into the Ollama pod's persistent volume using `kubectl exec`.
2.  Configured the Open WebUI service as a `NodePort` for LAN access.
3.  Reconfigured the **Cloudflare Tunnel** to point to the internal Kubernetes ClusterIP Service (`http://open-webui:80`), making the app securely accessible globally at `ai.polanatech.com`.

## Results and Next Steps

I successfully transitioned from an idle Mini PC to a functional MLOps infrastructure hosting a cutting-edge LLM, managed as **Infrastructure as Code (IaC)**.

Future steps for **Polana AI** include:
* Automating model updates via CI/CD pipelines.
* Implementing cluster resource monitoring with Prometheus and Grafana.
* Exploring local fine-tuning techniques on proprietary data.