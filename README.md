# ☁️ Azure CloudStart GmbH – Mini Project

![Status](https://img.shields.io/badge/status-in%20progress-yellow)
![Azure](https://img.shields.io/badge/cloud-Microsoft%20Azure-0078D4)
![Made by](https://img.shields.io/badge/made%20by-Emre%20Okay-blueviolet)

<a name="top"></a>
### 🌐 Choose your language / Wähle deine Sprache

<div align="center">

### [**EN — READ IN ENGLISH**](#english) &nbsp;&nbsp;|&nbsp;&nbsp; [🇩🇪 **AUF DEUTSCH LESEN**](#deutsch)

</div>

---
---

<a name="english"></a>
# EN — ENGLISH

## 📖 About this project

**CloudStart GmbH** is a fictional startup based in Vienna 🇦🇹 that just decided to move its entire IT infrastructure to the cloud. As the new Cloud Administrator, I (Emre) built a clean Azure environment for them — step by step, with security and best practices in mind.

📌 This is a **solo training project**, built as part of my Azure Weiterbildung at **DCI (Digital Career Institute)** in Germany.

---

## 🏢 The Scenario

| 🏷️ | Detail |
|---|---|
| 🏢 Company | CloudStart GmbH |
| 📍 Location | Vienna, Austria |
| 🌍 Azure Region | West Europe |
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
 ┗ 🌍 (Bonus) App Service → Web App
```

> *A detailed diagram (SVG) will be added here once the project is finished.*

---

## 🔧 What I built

### 1️⃣ Network Foundation 🌐
Created a Virtual Network with two separate subnets — one for applications, one for management — each protected by its own Network Security Group (NSG).

- ✅ VNet `vnet-cloudstart` (10.0.0.0/16)
- ✅ Subnet `snet-app` + NSG with RDP rule
- ✅ Subnet `snet-mgmt` + NSG with SSH rule

📸 Screenshots: [`/screenshots/a1-network`](./screenshots/a1-network)

---

### 2️⃣ Virtual Machines 🖥️🐧
Deployed one Windows Server VM and one Linux (Ubuntu) VM, each in its correct subnet. Connected to both via RDP and SSH.

- ✅ `vm-app01` — Windows Server 2022 (B1s)
- ✅ `vm-mgmt01` — Ubuntu Server 22.04 (B1s)

📸 Screenshots: [`/screenshots/a2-vms`](./screenshots/a2-vms)

---

### 3️⃣ Storage & Blob 🗄️
Set up a Storage Account with a private Blob Container, uploaded a test file, and generated a temporary secure link (SAS URL) to access it.

- ✅ Storage Account `stcloudstart...`
- ✅ Private Blob Container `dokumente`
- ✅ SAS URL (1 hour validity)

📸 Screenshots: [`/screenshots/a3-storage`](./screenshots/a3-storage)

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

📸 Screenshots: [`/screenshots/a4-entra-rbac`](./screenshots/a4-entra-rbac)

---

### 5️⃣ Monitoring 📊
Set up basic monitoring on the VM with a CPU metric chart and an alert rule that triggers an email if CPU usage gets too high.

- ✅ CPU metric chart (last hour)
- ✅ Alert Rule `alert-cpu-hoch` (>80% CPU → email)

📸 Screenshots: [`/screenshots/a5-monitoring`](./screenshots/a5-monitoring)

---

### 6️⃣ Security Check (Defender for Cloud) 🛡️
Reviewed the **Secure Score** and security recommendations in Microsoft Defender for Cloud. Found and fixed real security gaps — for example, restricting the open RDP rule instead of leaving it open to "Any".

> 💡 **Before:** RDP port open to the entire internet (`Any`)
> 💡 **After:** RDP port restricted to my own IP address

- ✅ Secure Score reviewed
- ✅ At least 1 recommendation fixed

📸 Screenshots: [`/screenshots/a6-defender`](./screenshots/a6-defender)

---

### ⭐ Bonus: App Service 🌍
Deployed a simple Web App on a free App Service Plan (F1 tier) to test PaaS deployment.

- ✅ App Service Plan `asp-cloudstart` (F1 Free)
- ✅ Web App `app-cloudstart-...`

📸 Screenshots: [`/screenshots/bonus-appservice`](./screenshots/bonus-appservice)

---

## 🏷️ Tagging Strategy

All resources are tagged consistently for clarity and cost tracking — good cloud hygiene, even in a training project.

| Tag | Value |
|---|---|
| `Project` | CloudStart-MiniProject |
| `Environment` | Demo |
| `Owner` | Emre Okay |
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
| 🌍 PaaS (Bonus) | App Service |

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

---

## 🎓 About me

I'm Emre, currently completing an IT System Administration & Cloud Engineering Weiterbildung at DCI (Digital Career Institute) in Germany, working towards a career as an Azure Administrator / Cloud Engineer.

🔗 More projects: [github.com/okayemre](https://github.com/okayemre)

---

## 📌 Status

🟡 **In Progress** — this README will be updated with final screenshots, results, and the architecture diagram once the project is complete.

<div align="right">

[⬆️ Back to language selector](#top)

</div>

---
---

<a name="deutsch"></a>
# 🇩🇪 DEUTSCH

## 📖 Über dieses Projekt

**CloudStart GmbH** ist ein fiktives Startup aus Wien 🇦🇹, das seine komplette IT in die Cloud verlagert. Als neuer Cloud-Administrator habe ich (Emre) für sie eine saubere Azure-Umgebung aufgebaut – Schritt für Schritt, mit Fokus auf Sicherheit und Best Practices.

📌 Dies ist ein **Solo-Trainingsprojekt**, entstanden im Rahmen meiner Azure-Weiterbildung am **DCI (Digital Career Institute)** in Deutschland.

---

## 🏢 Das Szenario

| 🏷️ | Detail |
|---|---|
| 🏢 Firma | CloudStart GmbH |
| 📍 Standort | Wien, Österreich |
| 🌍 Azure Region | West Europe |
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
 ┗ 🌍 (Bonus) App Service → Web App
```

> *Ein detailliertes Diagramm (SVG) wird hier ergänzt, sobald das Projekt fertig ist.*

---

## 🔧 Was ich gebaut habe

### 1️⃣ Netzwerk-Grundlage 🌐
Virtual Network mit zwei getrennten Subnetzen erstellt — eines für Anwendungen, eines für Verwaltung — jeweils mit eigener Network Security Group (NSG) geschützt.

- ✅ VNet `vnet-cloudstart` (10.0.0.0/16)
- ✅ Subnet `snet-app` + NSG mit RDP-Regel
- ✅ Subnet `snet-mgmt` + NSG mit SSH-Regel

📸 Screenshots: [`/screenshots/a1-network`](./screenshots/a1-network)

---

### 2️⃣ Virtuelle Maschinen 🖥️🐧
Eine Windows Server VM und eine Linux (Ubuntu) VM bereitgestellt, jeweils im richtigen Subnetz. Verbindung per RDP und SSH erfolgreich getestet.

- ✅ `vm-app01` — Windows Server 2022 (B1s)
- ✅ `vm-mgmt01` — Ubuntu Server 22.04 (B1s)

📸 Screenshots: [`/screenshots/a2-vms`](./screenshots/a2-vms)

---

### 3️⃣ Storage & Blob 🗄️
Storage Account mit privatem Blob Container eingerichtet, Testdatei hochgeladen und einen temporären sicheren Link (SAS URL) für den Zugriff erstellt.

- ✅ Storage Account `stcloudstart...`
- ✅ Privater Blob Container `dokumente`
- ✅ SAS URL (1 Stunde gültig)

📸 Screenshots: [`/screenshots/a3-storage`](./screenshots/a3-storage)

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

📸 Screenshots: [`/screenshots/a4-entra-rbac`](./screenshots/a4-entra-rbac)

---

### 5️⃣ Monitoring 📊
Basis-Monitoring auf der VM eingerichtet — CPU-Metrik-Diagramm plus Alert-Regel, die bei zu hoher CPU-Auslastung eine E-Mail auslöst.

- ✅ CPU-Metrik-Diagramm (letzte Stunde)
- ✅ Alert Rule `alert-cpu-hoch` (>80% CPU → E-Mail)

📸 Screenshots: [`/screenshots/a5-monitoring`](./screenshots/a5-monitoring)

---

### 6️⃣ Sicherheitscheck (Defender for Cloud) 🛡️
**Secure Score** und Sicherheitsempfehlungen in Microsoft Defender for Cloud überprüft. Echte Sicherheitslücken gefunden und behoben — zum Beispiel die offene RDP-Regel eingeschränkt, statt sie für "Any" offen zu lassen.

> 💡 **Vorher:** RDP-Port für das gesamte Internet offen (`Any`)
> 💡 **Nachher:** RDP-Port auf meine eigene IP-Adresse eingeschränkt

- ✅ Secure Score überprüft
- ✅ Mindestens 1 Empfehlung umgesetzt

📸 Screenshots: [`/screenshots/a6-defender`](./screenshots/a6-defender)

---

### ⭐ Bonus: App Service 🌍
Eine einfache Web App auf einem kostenlosen App Service Plan (F1 Tier) bereitgestellt, um PaaS-Deployment zu testen.

- ✅ App Service Plan `asp-cloudstart` (F1 Free)
- ✅ Web App `app-cloudstart-...`

📸 Screenshots: [`/screenshots/bonus-appservice`](./screenshots/bonus-appservice)

---

## 🏷️ Tag-Strategie

Alle Ressourcen sind einheitlich getaggt — für Übersicht und Kostenkontrolle, gute Cloud-Hygiene auch im Trainingsprojekt.

| Tag | Wert |
|---|---|
| `Project` | CloudStart-MiniProject |
| `Environment` | Demo |
| `Owner` | Emre Okay |
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
| 🌍 PaaS (Bonus) | App Service |

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

---

## 🎓 Über mich

Ich bin Emre und absolviere aktuell eine Weiterbildung zum IT System Administrator & Cloud Engineer am DCI (Digital Career Institute) in Deutschland — mit dem Ziel, als Azure Administrator / Cloud Engineer zu arbeiten.

🔗 Weitere Projekte: [github.com/okayemre](https://github.com/okayemre)

---

## 📌 Status

🟡 **In Bearbeitung** — dieses README wird nach Projektabschluss mit finalen Screenshots, Ergebnissen und dem Architektur-Diagramm aktualisiert.

<div align="right">

[⬆️ Zurück zur Sprachauswahl](#top)

</div>