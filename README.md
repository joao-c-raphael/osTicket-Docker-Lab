# osTicket-Docker-Lab
# Enterprise Ticketing System Homelab: osTicket on Docker (WSL2)

## 📌 Project Overview
This project details the deployment, troubleshooting, and validation of an **osTicket** web application running inside a Dockerized environment on Windows Subsystem for Linux (WSL2). 

The goal of this homelab is to demonstrate hands-on experience with:
- Containerized application deployment using **Docker** and **Docker Compose**.
- Environment configuration and lifecycle management via **PowerShell** and **WSL2**.
- Diagnostic troubleshooting using application and container logs (`docker compose ps`, `docker logs`).
- Operational workflows within an ITSM/Helpdesk platform (ticket submission, agent routing, and resolution).

---

## 🛠️ Prerequisites & Environment Setup

### 1. Software Requirements
- **Docker Desktop** (Engine & Compose)
- **Windows Subsystem for Linux 2 (WSL2)** enabled via PowerShell

### 2. Directory & Environment Configuration
1. Open PowerShell and navigate to your workspace to create the project directory:
   ```powershell
   mkdir osTicket-lab
   cd osTicket-lab
