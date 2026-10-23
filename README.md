# osTicket Docker Lab

## 📌 Project Overview
This project details the deployment, troubleshooting, and validation of an osTicket web application running inside a Dockerized environment on Windows Subsystem for Linux (WSL). 

The goal of this homelab is to demonstrate hands-on experience with:
- Containerized application deployment using Docker and Docker Compose.
- Environment configuration and lifecycle management via PowerShell and WSL2.
- Diagnostic troubleshooting using application and container logs (`docker compose ps`, `docker logs`).
- Operational workflows within an ITSM/Helpdesk platform (ticket submission, agent routing, and resolution).

---

## 🛠️ Prerequisites & Environment Setup

### 1. Software Requirements
- Docker Desktop (Engine & Compose)
- Windows Subsystem for Linux 2 (WSL2) enabled via PowerShell

### 2. Directory & Environment Configuration
1. Open PowerShell and navigate to your workspace to create the project directory:
   (`mkdir osTicket-lab`, `cd osTicket-lab`)
   <img width="332" height="23" alt="image" src="https://github.com/user-attachments/assets/110b98fc-97ec-4ac9-a201-4057dba1a326" />

2. Create the environment configuration file (.env):                                                                                                                     
   <img width="557" height="153" alt="image" src="https://github.com/user-attachments/assets/1a598575-e7b3-4115-a408-285ac804ed93" />

3. Create the container orchestration profile (docker-compose.yml):
   <img width="655" height="836" alt="image" src="https://github.com/user-attachments/assets/4b9ef6ac-d06f-4060-b857-804ed0c61fc1" />


---

## 🚀 Deployment & Container Launch

Navigate to the project directory and launch the container stack in detached mode:
 (`cd osTicket-lab`, `docker compose up -d`)
                                                                                                                                                     
<img width="652" height="162" alt="image" src="https://github.com/user-attachments/assets/5109808f-31e4-45be-b122-65b9807b987d" />

---

## 🔍 Troubleshooting & Resolution Workflow

During the initial browser access attempt (`http://localhost`), the web interface failed to load. The following diagnostic steps were performed to identify and resolve the root cause:

### Step 1: Container Status Check
Checked the health and execution status of the running containers:
`docker compose ps`

*Observation:* The osTicket-app container was caught in an automatic restart loop (`Restarting`).

<img width="1447" height="165" alt="image" src="https://github.com/user-attachments/assets/109f5ed5-01cb-4ce4-acdf-b1be0ba58a91" />


### Step 2: Log Inspection
Extracted container execution logs to isolate the error:
`docker compose logs osTicket-app`

<img width="725" height="25" alt="image" src="https://github.com/user-attachments/assets/d7f402f5-f556-4d3a-9a11-de9cd4409ecb" />


### Step 3: Root Cause Analysis & Mitigation
- **Analysis:** (Pasted logs into AI) Log inspection indicated that environment variables defined in `.env` were not being properly read by the web container upon initialization.
- **Root Cause:** The `.env` configuration file was missing or mislocated relative to the `docker-compose.yml` manifest.
- **Remediation:**
  1. Stopped and pruned the broken container stack and associated volumes:
     `docker compose down -v`
  2. Re-created and validated the `.env` file directly inside the `osTicket-lab` directory.
  3. Re-launched the container stack (`docker compose up -d`).

Following remediation, the `osTicket-app` container stabilized, and the portal successfully rendered in the browser.

---

## ✅ Application Verification & Workflow Testing

### 1. User Support Portal Access
Verified end-user interface accessibility at `http://localhost`.

(placeholder for screenshot)
(placeholder for screenshot)

### 2. Ticket Lifecycle Demonstration
- **Ticket Submission:** Simulated an end-user submitting a technical support request via the public portal.
- **Agent Resolution:** Logged into the osTicket Staff/Admin control panel to review, assign, and respond to the submitted ticket.

(placeholder for screenshot)
