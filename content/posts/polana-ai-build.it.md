---
title: "Implementazione di Polana AI: Infrastruttura Locale con Kubernetes e Gemma 3"
date: 2026-01-03T22:00:00+01:00
draft: false
description: "Dettagli tecnici sul deploy di un'infrastruttura AI locale utilizzando K3s, Docker e modelli open-source, con accesso sicuro via Cloudflare Tunnel."
tags: ["MLOps", "Kubernetes", "K3s", "AI Locale", "Gemma 3", "Linux", "HomeLab"]
categories: ["Progetti", "Infrastruttura"]
---

## Il Contesto

Ho sviluppato un'infrastruttura locale dedicata alla gestione tecnica del ciclo di vita di applicazioni basate su Intelligenza Artificiale. L'obiettivo del progetto è l'ottimizzazione di risorse hardware locali per l'orchestrazione di container e modelli LLM in un ambiente scalabile e controllato.

## L'Architettura

Il progetto **Polana AI** si basa su un'architettura consolidata su hardware dedicato.

* **Hardware:** Mini PC Intel Core i7 con 16GB di RAM.
* **OS:** Ubuntu Server (headless).
* **Orchestrazione:** K3s (Lightweight Kubernetes) per la gestione certificata dei container.
* **AI Engine & UI:** Ollama per il serving del modello e Open WebUI per l'interfaccia utente.
* **Modello AI:** Google Gemma 3 4B.
* **Networking:** Cloudflare Zero Trust Tunnel per l'accesso sicuro dall'esterno senza esposizione di porte sul router.

## La Cronistoria del Build (3 Gennaio 2026)

### 1. Setup Sistema Operativo
Il build è iniziato con un'installazione pulita di Ubuntu Server, configurando il sistema per carichi di lavoro intensivi.

### 2. Configurazione Orchestrazione
Dopo i test iniziali su Docker, l'infrastruttura è stata migrata su **Kubernetes (K3s)** per una gestione avanzata dei carichi.
* **Risoluzione Conflitti:** Durante la migrazione è stato risolto un conflitto di porte tra i processi Docker e i Pod Kubernetes.
* **Manutenzione:** Eseguito audit dei processi (`ps aux`) e pulizia del sistema (`docker system prune`, `ncdu`) per ottimizzare lo spazio su disco.

### 3. Deploy e Networking
* Inizializzazione del modello **Gemma 3 4B** nel volume persistente del pod Ollama tramite `kubectl exec`.
* Configurazione di Open WebUI come `NodePort` per l'accesso in rete locale.
* Mapping del **Cloudflare Tunnel** verso il Service ClusterIP interno (`http://open-webui:80`) per l'accesso globale su `ai.polanatech.com`.

## Risultati e Sviluppi Tecnici

L'infrastruttura è attualmente operativa e gestita secondo il paradigma Infrastructure as Code.

I prossimi sviluppi includono:
* Automazione dei cicli di aggiornamento dei modelli tramite pipeline CI/CD.
* Implementazione del monitoraggio delle risorse con Prometheus e Grafana.
* Test di integrazione dati locali per il modello LLM.