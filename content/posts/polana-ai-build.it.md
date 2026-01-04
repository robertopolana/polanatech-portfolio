---
title: "Building Polana AI: Da Zero a MLOps Locale con Kubernetes e Gemma 3"
date: 2026-01-03T22:00:00+01:00
draft: false
description: "Come ho trasformato un Mini PC in un'infrastruttura AI di produzione usando K3s, Docker e modelli open-source, con accesso globale via Cloudflare Tunnel."
tags: ["MLOps", "Kubernetes", "K3s", "AI Locale", "Gemma 3", "Linux", "HomeLab"]
categories: ["Progetti", "Infrastruttura"]
---

## Il Contesto

Nel mio percorso di specializzazione come **IT Specialist** verso ruoli **MLOps**, ho deciso di costruire un'infrastruttura locale per gestire l'intero ciclo di vita di un'applicazione basata su Intelligenza Artificiale. L'obiettivo era passare dalla teoria alla pratica, orchestrando container e modelli LLM in un ambiente controllato ma scalabile.

## L'Architettura

Il progetto **Polana AI** non è solo un'installazione software, è un'architettura completa costruita su hardware commodity.

* **Hardware:** Mini PC Intel Core i7 con 16GB di RAM.
* **OS:** Ubuntu Server (headless) per massimizzare le risorse.
* **Orchestrazione:** K3s (Lightweight Kubernetes) per una gestione efficiente e certificata dei container.
* **AI Engine & UI:** Ollama per il serving del modello e Open WebUI per l'interfaccia utente.
* **Modello AI:** Google Gemma 3 4B (il nuovo standard del 2026 per efficienza).
* **Networking:** Cloudflare Zero Trust Tunnel per l'accesso sicuro dall'esterno senza esporre porte sul router.

## La Cronistoria del Build (3 Gennaio 2026)

### 1. L'Installazione "Bare Metal"
La giornata è iniziata con un'installazione pulita di Ubuntu Server tramite chiavetta USB, preparando il "ferro" per il suo nuovo ruolo.

### 2. La Transizione verso l'Orchestrazione
Ho inizialmente testato il deploy tramite Docker classico. Tuttavia, per allinearmi alle best practice MLOps, ho deciso di migrare rapidamente a **Kubernetes (K3s)**.
* **Sfida Tecnica:** Durante la migrazione, si è creato un conflitto di porte tra i vecchi processi Docker e i nuovi Pod Kubernetes.
* **Risoluzione:** Ho eseguito un audit dei processi con `ps aux` e `docker ps`, terminato i vecchi container e pulito il sistema con `docker system prune` e `ncdu` per recuperare spazio su disco, lasciando il campo libero a K3s.

### 3. Deploy e Configurazione
Una volta stabilizzato il cluster K3s:
1.  Ho eseguito il pull del modello **Gemma 3 4B** direttamente nel volume persistente del pod Ollama con `kubectl exec`.
2.  Ho configurato il servizio Open WebUI come `NodePort` per l'accesso LAN.
3.  Ho riconfigurato il **Cloudflare Tunnel** per puntare al Service ClusterIP interno di Kubernetes (`http://open-webui:80`), rendendo l'applicazione accessibile globalmente e in sicurezza su `ai.polanatech.com`.

## Risultati e Prossimi Passi

Quindi sono passato da un Mini PC spento a un'infrastruttura MLOps funzionante che ospita un LLM all'avanguardia, gestita come codice (Infrastructure as Code).

I prossimi step per **Polana AI** includono:
* Automatizzare l'aggiornamento dei modelli tramite pipeline CI/CD.
* Implementare il monitoraggio delle risorse del cluster con Prometheus e Grafana.
* Esplorare tecniche di *fine-tuning* locale sui miei dati.