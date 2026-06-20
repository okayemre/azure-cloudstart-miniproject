# ☁️ Azure CloudStart GmbH – Mini Project

![Status](https://img.shields.io/badge/status-complete-brightgreen)
![Azure](https://img.shields.io/badge/cloud-Microsoft%20Azure-0078D4)

![Virtual Network](https://img.shields.io/badge/Virtual%20Network-0078D4?logo=microsoftazure&logoColor=white)
![Virtual Machines](https://img.shields.io/badge/Virtual%20Machines-0078D4?logo=microsoftazure&logoColor=white)
![Storage](https://img.shields.io/badge/Blob%20Storage-0078D4?logo=microsoftazure&logoColor=white)
![Entra ID](https://img.shields.io/badge/Microsoft%20Entra%20ID-0078D4?logo=microsoftazure&logoColor=white)
![Monitor](https://img.shields.io/badge/Azure%20Monitor-0078D4?logo=microsoftazure&logoColor=white)
![Defender](https://img.shields.io/badge/Defender%20for%20Cloud-0078D4?logo=microsoftazure&logoColor=white)
![App Service](https://img.shields.io/badge/App%20Service-0078D4?logo=microsoftazure&logoColor=white)

<a name="top"></a>
### 🌐 Choose your language / Wähle deine Sprache

<div align="center">

### [**Read in English**](#english) &nbsp;&nbsp;|&nbsp;&nbsp; [**Auf Deutsch lesen**](#deutsch)

</div>

---
---

<a name="english"></a>
# English

## 📖 About this project

**CloudStart GmbH** is a fictional startup based in Vienna 🇦🇹 that just decided to move its entire IT infrastructure to the cloud. As the new Cloud Administrator, I (Emre) built a clean Azure environment for them — step by step, with security and best practices in mind.

📌 This is a **solo training project**, built as part of my Azure Weiterbildung at **DCI (Digital Career Institute)** in Germany.

---

## 🏢 The Scenario

| 🏷️ | Detail |
|---|---|
| 🏢 Company | CloudStart GmbH |
| 📍 Location | Vienna, Austria |
| 🌍 Azure Region | Sweden Central |
| 📦 Resource Group | `rg-cloudstart` |
| 👥 Employees | 3 fictional users with different access levels |

The goal: build a small but realistic company IT setup in Azure — with proper network segmentation, role-based access (RBAC), monitoring, and security checks.

---

## 🗺️ Architecture Overview

```
📦 rg-cloudstart
 ┣ 🌐 vnet-cloudstart (10.0.0.0/16)
 ┃  ┣ 🟦 snet-app (10.0.1.0/24)   → 🛡️ nsg-app  → 🖥️ vm-app01 (Windows)
 ┃  ┗ 🟩 snet-mgmt (10.0.2.0/24)  → 🛡️ nsg-mgmt → 🐧 vm-mgmt01 (Linux)
 ┣ 🗄️ Storage Account → 📁 Blob Container "dokumente"
 ┣ 👤 Microsoft Entra ID → Users + Group + RBAC
 ┣ 📊 Azure Monitor → CPU Alert
 ┣ 🛡️ Microsoft Defender for Cloud → Secure Score + Recommendations
 ┗ 🌍 App Service → Web App
```

📐 Visual diagram:

![Architecture Diagram](./docs/architecture-diagram.svg)

---

## 🔧 What I built

### 1️⃣ Network Foundation 🌐
Created a Virtual Network with two separate subnets — one for applications, one for management — each protected by its own Network Security Group (NSG).

- ✅ VNet `vnet-cloudstart` (10.0.0.0/16)
- ✅ Subnet `snet-app` + NSG with RDP rule
- ✅ Subnet `snet-mgmt` + NSG with SSH rule

📸
| nsg-app — Inbound Rules | nsg-mgmt — Inbound Rules |
|---|---|
| ![nsg-app inbound rules](./screenshots/a1-network/01-nsg-app-inbound-rules.png) | ![nsg-mgmt inbound rules](./screenshots/a1-network/02-nsg-mgmt-inbound-rules.png) |

---

### 2️⃣ Virtual Machines 🖥️🐧
Deployed one Windows Server VM and one Linux (Ubuntu) VM, each in its correct subnet. Connected to both via RDP and SSH.

- ✅ `vm-app01` — Windows Server 2022 (B1s)
- ✅ `vm-mgmt01` — Ubuntu Server 24.04 (B1s)

📸
| RDP → Server Manager (vm-app01) | SSH → uname -a (vm-mgmt01) |
|---|---|
| ![Server Manager vm-app01](./screenshots/a2-vms/01-server-manager-vm-app01.png) | ![SSH connection vm-mgmt01](./screenshots/a2-vms/02-ssh-connection-vm-mgmt01.png) |

---

### 3️⃣ Storage & Blob 🗄️
Set up a Storage Account with a private Blob Container, uploaded a test file, and generated a temporary secure link (SAS URL) to access it.

- ✅ Storage Account `stcloudstartmr`
- ✅ Private Blob Container `dokumente`
- ✅ SAS URL (1 hour validity)

📸
| Blob Container (Private) | SAS URL opened in browser |
|---|---|
| ![Blob container dokumente](./screenshots/a3-storage/01-blob-container-dokumente.png) | ![SAS URL test](./screenshots/a3-storage/02-sas-url-test.png) |

---

### 4️⃣ Identity & Access (Entra ID + RBAC) 👤🔐
Created 3 fictional users in Microsoft Entra ID, grouped them, and assigned **least-privilege** access using RBAC roles.

| 👤 User | 🎭 Role | 🔑 Access |
|---|---|---|
| Anna Maier | CEO | Reader (read-only) |
| Ben Koller | Developer | VM Contributor (via group) |
| Clara Fuchs | Intern | No Azure access |

- ✅ Security Group `grp-entwickler`
- ✅ RBAC roles assigned on Resource Group level

📸
![Entra ID Users](./screenshots/a4-entra-rbac/01-entra-id-users.png)

| Group Members (grp-entwickler) | RBAC Role Assignments |
|---|---|
| ![Group members](./screenshots/a4-entra-rbac/02-group-members-grp-entwickler.png) | ![RBAC role assignments](./screenshots/a4-entra-rbac/03-rbac-role-assignments.png) |

---

### 5️⃣ Monitoring 📊
Set up basic monitoring on the VM with a CPU metric chart and an alert rule that triggers an email if CPU usage gets too high.

- ✅ CPU metric chart (last hour)
- ✅ Alert Rule `alert-cpu-hoch` (>80% CPU → email, Severity 2)

📸
| CPU Metric Chart | Alert Rule Configuration |
|---|---|
| ![CPU metric chart](./screenshots/a5-monitoring/01-cpu-metric-chart.png) | ![Alert rule config](./screenshots/a5-monitoring/02-alert-rule-config.png) |

---

### 6️⃣ Security Check (Defender for Cloud) 🛡️
Reviewed the **Secure Score** in Microsoft Defender for Cloud (Foundational CSPM, free tier).

- ✅ Secure Score reviewed (**31%**)
- ⚠️ Recommendations review & fix: **not completed** — Defender's resource inventory had not finished syncing the newly created resources (`vm-app01`, `vm-mgmt01`, NSGs, Storage Account) within the project timeframe, even though the Foundational CSPM plan was active with full coverage. This is a known sync-delay behavior on fresh Azure for Students subscriptions.

📸
![Secure Score](./screenshots/a6-defender/01-secure-score.png)

> 💡 **Lesson learned:** Defender for Cloud's recommendation engine can take several hours (sometimes up to 24h) to fully index brand-new resources, even when the plan itself is active immediately. Planning security reviews a day after resource creation — rather than back-to-back — would avoid this gap.

---

### ⭐ App Service 🌍
Deployed a Web App on a free App Service Plan (F1 tier) to test PaaS deployment.

- ✅ App Service Plan `asp-cloudstart` (F1 Free)
- ✅ Web App `app-cloudstart-mr`
- ✅ Application Setting `UMGEBUNG = Test`

📸
| Web App running | Application Setting |
|---|---|
| ![Web app default page](./screenshots/bonus-appservice/01-webapp-default-page.png) | ![App setting UMGEBUNG](./screenshots/bonus-appservice/02-app-setting-umgebung.png) |

> 💡 **Debugging note:** The first deployment attempt (Windows + Node 24 LTS runtime) failed with *"64 Bit worker processes cannot be used... as the plan does not allow it"* — Node 24 LTS requires a 64-bit worker process on Windows, which the F1 (Free) tier doesn't support. Switching the runtime stack to **.NET** resolved it immediately, since .NET on Windows F1 defaults to a compatible 32-bit worker process.

---

## 🏷️ Tagging Strategy

All resources are tagged consistently for clarity and cost tracking — good cloud hygiene, even in a training project.

| Tag | Value |
|---|---|
| `Project` | CloudStart-MiniProject |
| `Environment` | Training |
| `Owner` | Emre |
| `CostCenter` | Student-Credit |
| `ManagedBy` | Manual |
| `DeleteAfter` | 2026-06-30 |

---

## 🛠️ Azure Services Used

| Category | Service |
|---|---|
| 🌐 Networking | Virtual Network, Subnets, NSGs |
| 🖥️ Compute | Virtual Machines (Windows & Linux) |
| 🗄️ Storage | Storage Account, Blob Container, SAS |
| 👤 Identity | Microsoft Entra ID, RBAC |
| 📊 Monitoring | Azure Monitor, Alert Rules |
| 🛡️ Security | Microsoft Defender for Cloud |
| 🌍 PaaS | App Service |

---

## 💰 Cost Note

This project was built within the limits of an Azure for Students subscription. Cheapest VM sizes (B1s) and free-tier services (F1 App Service) were used wherever possible. All resources were deleted after project completion to save credit.

---

## 📂 Repository Structure

```
azure-cloudstart-miniproject/
├── README.md
├── .gitignore
├── screenshots/
│   ├── a1-network/
│   ├── a2-vms/
│   ├── a3-storage/
│   ├── a4-entra-rbac/
│   ├── a5-monitoring/
│   ├── a6-defender/
│   └── bonus-appservice/
└── docs/
    └── architecture-diagram.svg
```

<div align="right">

[⬆️ Back to language selector](#top)

</div>

---
---

<a name="deutsch"></a>
# Deutsch

## 📖 Über dieses Projekt

**CloudStart GmbH** ist ein fiktives Startup aus Wien 🇦🇹, das seine komplette IT in die Cloud verlagert. Als neuer Cloud-Administrator habe ich (Emre) für sie eine saubere Azure-Umgebung aufgebaut – Schritt für Schritt, mit Fokus auf Sicherheit und Best Practices.

📌 Dies ist ein **Solo-Trainingsprojekt**, entstanden im Rahmen meiner Azure-Weiterbildung am **DCI (Digital Career Institute)** in Deutschland.

---

## 🏢 Das Szenario

| 🏷️ | Detail |
|---|---|
| 🏢 Firma | CloudStart GmbH |
| 📍 Standort | Wien, Österreich |
| 🌍 Azure Region | Sweden Central |
| 📦 Resource Group | `rg-cloudstart` |
| 👥 Mitarbeiter | 3 fiktive Benutzer mit unterschiedlichen Zugriffsrechten |

Das Ziel: ein kleines, aber realistisches Firmen-IT-Setup in Azure aufbauen – mit sauberer Netzwerk-Trennung, rollenbasiertem Zugriff (RBAC), Monitoring und Sicherheitschecks.

---

## 🗺️ Architektur-Übersicht

```
📦 rg-cloudstart
 ┣ 🌐 vnet-cloudstart (10.0.0.0/16)
 ┃  ┣ 🟦 snet-app (10.0.1.0/24)   → 🛡️ nsg-app  → 🖥️ vm-app01 (Windows)
 ┃  ┗ 🟩 snet-mgmt (10.0.2.0/24)  → 🛡️ nsg-mgmt → 🐧 vm-mgmt01 (Linux)
 ┣ 🗄️ Storage Account → 📁 Blob Container "dokumente"
 ┣ 👤 Microsoft Entra ID → Users + Group + RBAC
 ┣ 📊 Azure Monitor → CPU Alert
 ┣ 🛡️ Microsoft Defender for Cloud → Secure Score + Empfehlungen
 ┗ 🌍 App Service → Web App
```

📐 Visuelles Diagramm:

![Architektur-Diagramm](./docs/architecture-diagram.svg)

---

## 🔧 Was ich gebaut habe

### 1️⃣ Netzwerk-Grundlage 🌐
Virtual Network mit zwei getrennten Subnetzen erstellt — eines für Anwendungen, eines für Verwaltung — jeweils mit eigener Network Security Group (NSG) geschützt.

- ✅ VNet `vnet-cloudstart` (10.0.0.0/16)
- ✅ Subnet `snet-app` + NSG mit RDP-Regel
- ✅ Subnet `snet-mgmt` + NSG mit SSH-Regel

📸
| nsg-app — Inbound Rules | nsg-mgmt — Inbound Rules |
|---|---|
| ![nsg-app inbound rules](./screenshots/a1-network/01-nsg-app-inbound-rules.png) | ![nsg-mgmt inbound rules](./screenshots/a1-network/02-nsg-mgmt-inbound-rules.png) |

---

### 2️⃣ Virtuelle Maschinen 🖥️🐧
Eine Windows Server VM und eine Linux (Ubuntu) VM bereitgestellt, jeweils im richtigen Subnetz. Verbindung per RDP und SSH erfolgreich getestet.

- ✅ `vm-app01` — Windows Server 2022 (B1s)
- ✅ `vm-mgmt01` — Ubuntu Server 24.04 (B1s)

📸
| RDP → Server Manager (vm-app01) | SSH → uname -a (vm-mgmt01) |
|---|---|
| ![Server Manager vm-app01](./screenshots/a2-vms/01-server-manager-vm-app01.png) | ![SSH Verbindung vm-mgmt01](./screenshots/a2-vms/02-ssh-connection-vm-mgmt01.png) |

---

### 3️⃣ Storage & Blob 🗄️
Storage Account mit privatem Blob Container eingerichtet, Testdatei hochgeladen und einen temporären sicheren Link (SAS URL) für den Zugriff erstellt.

- ✅ Storage Account `stcloudstartmr`
- ✅ Privater Blob Container `dokumente`
- ✅ SAS URL (1 Stunde gültig)

📸
| Blob Container (Privat) | SAS URL im Browser geöffnet |
|---|---|
| ![Blob Container dokumente](./screenshots/a3-storage/01-blob-container-dokumente.png) | ![SAS URL Test](./screenshots/a3-storage/02-sas-url-test.png) |

---

### 4️⃣ Identity & Zugriff (Entra ID + RBAC) 👤🔐
3 fiktive Benutzer in Microsoft Entra ID erstellt, gruppiert und Zugriff nach dem **Least-Privilege-Prinzip** über RBAC-Rollen vergeben.

| 👤 Benutzer | 🎭 Rolle | 🔑 Zugriff |
|---|---|---|
| Anna Maier | Geschäftsführerin | Reader (nur Lesezugriff) |
| Ben Koller | Entwickler | VM Contributor (über Gruppe) |
| Clara Fuchs | Praktikantin | Kein Azure-Zugriff |

- ✅ Sicherheitsgruppe `grp-entwickler`
- ✅ RBAC-Rollen auf Resource-Group-Ebene zugewiesen

📸
![Entra ID Benutzer](./screenshots/a4-entra-rbac/01-entra-id-users.png)

| Gruppenmitglieder (grp-entwickler) | RBAC-Rollenzuweisungen |
|---|---|
| ![Gruppenmitglieder](./screenshots/a4-entra-rbac/02-group-members-grp-entwickler.png) | ![RBAC Rollenzuweisungen](./screenshots/a4-entra-rbac/03-rbac-role-assignments.png) |

---

### 5️⃣ Monitoring 📊
Basis-Monitoring auf der VM eingerichtet — CPU-Metrik-Diagramm plus Alert-Regel, die bei zu hoher CPU-Auslastung eine E-Mail auslöst.

- ✅ CPU-Metrik-Diagramm (letzte Stunde)
- ✅ Alert Rule `alert-cpu-hoch` (>80% CPU → E-Mail, Severity 2)

📸
| CPU-Metrik-Diagramm | Alert Rule Konfiguration |
|---|---|
| ![CPU Metrik Diagramm](./screenshots/a5-monitoring/01-cpu-metric-chart.png) | ![Alert Rule Konfiguration](./screenshots/a5-monitoring/02-alert-rule-config.png) |

---

### 6️⃣ Sicherheitscheck (Defender for Cloud) 🛡️
**Secure Score** in Microsoft Defender for Cloud überprüft (Foundational CSPM, kostenloser Tier).

- ✅ Secure Score überprüft (**31%**)
- ⚠️ Empfehlungen prüfen & umsetzen: **nicht abgeschlossen** — Defenders Ressourcen-Inventar hatte die neu erstellten Ressourcen (`vm-app01`, `vm-mgmt01`, NSGs, Storage Account) innerhalb des Projektzeitraums noch nicht vollständig synchronisiert, obwohl der Foundational-CSPM-Plan aktiv war und volle Abdeckung zeigte. Dies ist ein bekanntes Synchronisierungsverhalten bei frischen Azure-for-Students-Subscriptions.

📸
![Secure Score](./screenshots/a6-defender/01-secure-score.png)

> 💡 **Erkenntnis:** Defender for Cloud's Empfehlungs-Engine kann mehrere Stunden (manchmal bis zu 24h) brauchen, um brandneue Ressourcen vollständig zu indexieren — auch wenn der Plan selbst sofort aktiv ist. Sicherheitsüberprüfungen einen Tag nach der Ressourcenerstellung einzuplanen, statt direkt im Anschluss, würde diese Lücke vermeiden.

---

### ⭐ App Service 🌍
Eine Web App auf einem kostenlosen App Service Plan (F1 Tier) bereitgestellt, um PaaS-Deployment zu testen.

- ✅ App Service Plan `asp-cloudstart` (F1 Free)
- ✅ Web App `app-cloudstart-mr`
- ✅ Application Setting `UMGEBUNG = Test`

📸
| Web App läuft | Application Setting |
|---|---|
| ![Web App Standardseite](./screenshots/bonus-appservice/01-webapp-default-page.png) | ![App Setting UMGEBUNG](./screenshots/bonus-appservice/02-app-setting-umgebung.png) |

> 💡 **Debugging-Hinweis:** Der erste Deployment-Versuch (Windows + Node 24 LTS Runtime) schlug fehl mit *"64 Bit worker processes cannot be used... as the plan does not allow it"* — Node 24 LTS benötigt unter Windows einen 64-Bit-Worker-Prozess, den der F1-(Free)-Tier nicht unterstützt. Der Wechsel der Runtime auf **.NET** löste das Problem sofort, da .NET unter Windows F1 standardmäßig einen kompatiblen 32-Bit-Worker-Prozess verwendet.

---

## 🏷️ Tag-Strategie

Alle Ressourcen sind einheitlich getaggt — für Übersicht und Kostenkontrolle, gute Cloud-Hygiene auch im Trainingsprojekt.

| Tag | Wert |
|---|---|
| `Project` | CloudStart-MiniProject |
| `Environment` | Training |
| `Owner` | Emre |
| `CostCenter` | Student-Credit |
| `ManagedBy` | Manual |
| `DeleteAfter` | 2026-06-30 |

---

## 🛠️ Verwendete Azure-Dienste

| Kategorie | Dienst |
|---|---|
| 🌐 Netzwerk | Virtual Network, Subnets, NSGs |
| 🖥️ Compute | Virtuelle Maschinen (Windows & Linux) |
| 🗄️ Storage | Storage Account, Blob Container, SAS |
| 👤 Identity | Microsoft Entra ID, RBAC |
| 📊 Monitoring | Azure Monitor, Alert Rules |
| 🛡️ Security | Microsoft Defender for Cloud |
| 🌍 PaaS | App Service |

---

## 💰 Kostenhinweis

Dieses Projekt wurde innerhalb der Grenzen eines Azure for Students Abos umgesetzt. Wo möglich wurden die günstigsten VM-Größen (B1s) und kostenlose Dienste (F1 App Service) verwendet. Alle Ressourcen wurden nach Projektabschluss gelöscht, um Credits zu sparen.

---

## 📂 Repository-Struktur

```
azure-cloudstart-miniproject/
├── README.md
├── .gitignore
├── screenshots/
│   ├── a1-network/
│   ├── a2-vms/
│   ├── a3-storage/
│   ├── a4-entra-rbac/
│   ├── a5-monitoring/
│   ├── a6-defender/
│   └── bonus-appservice/
└── docs/
    └── architecture-diagram.svg
```

<div align="right">

[⬆️ Zurück zur Sprachauswahl](#top)

</div>