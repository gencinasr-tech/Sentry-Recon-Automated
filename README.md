# 🛡️ Sentry Recon: Automated Bug Bounty Pipeline

![Version](https://img.shields.io/badge/version-1.0.0-blue) ![Platform](https://img.shields.io/badge/platform-Linux%20%7C%20Docker-lightgrey) ![License](https://img.shields.io/badge/license-MIT-green)

> **[EN]** Automated reconnaissance and vulnerability detection system hosted on a Home Lab.
>
> **[ES]** Sistema de reconocimiento automatizado y detección de vulnerabilidades alojado en Home Lab.

---

## 🌍 Language / Idioma

- [🇺🇸 English Version](#-english-version)
- [🇪🇸 Versión en Español](#-versión-en-español)

---

## 🇺🇸 English Version

### 📋 Overview
**Sentry Recon** is a continuous security pipeline designed to automate the repetitive phases of Bug Bounty (Reconnaissance & Fuzzing). Hosted on a **Proxmox** server using LXC containers, it runs 24/7 to identify new assets and low-hanging fruit vulnerabilities.

### 🚀 Key Features
- **Continuous Monitoring:** Daily cron jobs to detect new subdomains.
- **Smart Filtering:** Automatically discards noise (404s) and focuses on live assets (200/403).
- **Real-time Alerting:** Integrated with Telegram API for instant notifications.
- **Modular Design:** Built with Bash scripts wrapping industry-standard tools (Nuclei, Subfinder, Httpx).

### 📂 Project Structure
- '/scripts': Core bash scripts for the automation pipeline.
- '/docs': Architecture diagrams and installation guides.
- '/case-studies': Real-world vulnerability reports found using this system.

### 🏆 Featured Case Study
> **Target:** Ford (VDP)
> **Vulnerability:** Broken Access Control on Pre-Launch Environment.
> **Result:** Unauthorized access to premium infotainment services.
> [Read full report here](case-studies/01_FORD_Karaoke_Access.md)

---

## 🇪🇸 Versión en Español

### 📋 Resumen
**Sentry Recon** es un pipeline de seguridad continuo diseñado para automatizar las fases repetitivas del Bug Bounty. Alojado en un servidor **Proxmox** usando contenedores LXC, funciona 24/7 para identificar nuevos activos.

### 🚀 Características Principales
- **Monitoreo Continuo:** Tareas cron diarias para detectar nuevos subdominios.
- **Filtrado Inteligente:** Descarta automáticamente el ruido (404s).
- **Alertas en Tiempo Real:** Integrado con la API de Telegram.
- **Diseño Modular:** Scripts de Bash que orquestan herramientas estándar.

### 📂 Estructura del Proyecto
- '/scripts': Scripts principales del pipeline.
- '/docs': Documentación de arquitectura.
- '/case-studies': Reportes de vulnerabilidades reales (como el caso Ford).

### 🏆 Caso de Estudio Destacado
> **Objetivo:** Ford (VDP)
> **Vulnerabilidad:** Broken Access Control en Entorno de Pre-Lanzamiento.
> **Resultado:** Acceso no autorizado a servicios premium de infoentretenimiento.
> [Leer reporte completo aquí](case-studies/01_FORD_Karaoke_Access.md)

---
*Created by gencinasr-tech - 2026*
