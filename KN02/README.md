# 1.Teil / Cloud Computing – Teil-Challenge

## 1. Aufgabe: Begriffe zuordnen

| Beschreibung                                   | Cloud-Service-Modell |
|-----------------------------------------------|---------------------|
| Hosting von virtuellen Maschinen              | **IaaS**            |
| Nutzung von Google Docs für Textbearbeitung   | **SaaS**            |
| Containerverwaltung mit Kubernetes            | **CaaS**            |

---

## 2. Aufgabe: Unterschied zwischen IaaS und PaaS

### 🔹 IaaS (Infrastructure as a Service)

Bei **IaaS** stellt der Anbieter grundlegende Infrastruktur zur Verfügung:
- Virtuelle Maschinen
- Netzwerk
- Speicher

👉 **Der Benutzer ist verantwortlich für:**
- Betriebssystem installieren und konfigurieren
- Software installieren
- Updates und Sicherheit
- Laufende Wartung

👉 Beispiel:
- AWS EC2
- Microsoft Azure VM

---

### 🔹 PaaS (Platform as a Service)

Bei **PaaS** stellt der Anbieter eine fertige Plattform bereit:
- Betriebssystem
- Laufzeitumgebung (z.B. Java, .NET)
- Datenbanken und Tools

👉 **Der Benutzer ist verantwortlich für:**
- Eigene Anwendung (Code)
- Konfiguration der App

👉 **Nicht mehr notwendig:**
- OS-Management
- Server-Wartung

👉 Beispiel:
- Heroku
- Google App Engine

---

## 🔁 Hauptunterschied

| IaaS                          | PaaS                          |
|------------------------------|------------------------------|
| Mehr Kontrolle               | Weniger Kontrolle            |
| Mehr Verantwortung           | Weniger Verantwortung        |
| OS & Infrastruktur selbst    | Plattform wird bereitgestellt|

---

## 🧠 Fazit

- **IaaS** = maximale Kontrolle, aber mehr Aufwand  
- **PaaS** = weniger Aufwand, Fokus auf Entwicklung  
- **SaaS** = fertige Anwendung (z.B. Google Docs)  
- **CaaS** = Container-basierte Infrastruktur (z.B. Kubernetes)

---

## 📌 Ziel erreicht

✔ Cloud-Modelle verstanden  
✔ Dienste korrekt zugeordnet  
✔ Unterschiede zwischen IaaS und PaaS erklärt  
✔ Dokumentation im Repository festgehalten  




# ⚙️ Teil 2 / Infrastructure as Code (IaC)

## 📌 1. Aufgabe: Automatisierung vs. Manuelle Konfiguration

### ❓ Warum ist Automatisierung besser als manuelle Konfiguration?

- **Schneller** → Systeme können in Sekunden/Minuten bereitgestellt werden  
- **Weniger Fehler** → menschliche Fehler werden reduziert  
- **Wiederholbar** → gleiche Konfiguration jederzeit reproduzierbar  
- **Skalierbar** → mehrere Systeme gleichzeitig aufsetzen  
- **Effizient** → weniger manuelle Arbeit, mehr Fokus auf wichtige Aufgaben  
- **Stabil** → getestete Konfigurationen werden immer gleich angewendet  

---

### ❓ Was bedeutet Infrastructure as Code (IaC)?

**Definition:**

Infrastructure as Code (IaC) bedeutet, dass IT-Infrastruktur (Server, Netzwerke, etc.) **als Code in Dateien beschrieben** wird.

👉 Diese Dateien:
- werden automatisch ausgeführt  
- sind versioniert (z.B. Git)  
- können getestet und wiederverwendet werden  

👉 Ziel:
- **Automatisierung**
- **Standardisierung**
- **Nachvollziehbarkeit**

---

## 🛠️ 2. Aufgabe: Tools und Konzepte

### 🔹 Tool 1: Docker

- Plattform zur **Containerisierung von Anwendungen**
- Verpackt Anwendung + Abhängigkeiten in Container
- Läuft überall gleich (Laptop, Server, Cloud)

👉 **Use Case:**
- Web-App schnell starten ohne komplizierte Installation

---

### 🔹 Tool 2: Terraform

- Tool zur **automatischen Bereitstellung von Infrastruktur**
- Ressourcen werden als Code definiert (z.B. Server, Netzwerke)

👉 Beispiel:
- AWS-Server automatisch erstellen

👉 Vorteile:
- Wiederholbar
- Versionskontrolle möglich

---

## ☸️ Kubernetes & Container-Orchestrierung

### 🔹 Kubernetes

- Open-Source-Plattform zur **Verwaltung von Containern**
- Automatisiert Deployment, Skalierung und Betrieb

---

### 🔹 Container-Orchestrierung (Stichpunkte)

- Verwaltung vieler Container gleichzeitig  
- Automatisches Starten/Stoppen von Containern  
- **Skalierung** (mehr/weniger Container je nach Bedarf)  
- **Load Balancing** (Verteilung der Last)  
- **Self-Healing** (defekte Container werden neu gestartet)  
- **Rollouts & Updates** ohne Downtime  

---

## 🧠 Verständnis (eigene Zusammenfassung)

- IaC macht Infrastruktur **programmierbar**
- Docker macht Anwendungen **portabel**
- Kubernetes verwaltet Container **automatisch und effizient**

---

## 📌 Ziel erreicht

✔ Automatisierung vs. manuell verstanden  
✔ IaC erklärt  
✔ Tools (Docker, Terraform) verstanden  
✔ Kubernetes & Orchestrierung erklärt  
✔ Dokumentation im Repository ergänzt  



# ☁️ 3 Teil / Cloud Plattformen Vergleich

## 📊 1. Aufgabe: Globale Infrastruktur vergleichen

| Plattform | Regionen weltweit | Verfügbarkeitszonen (AZs) | Besonderheiten |
|----------|------------------|--------------------------|----------------|
| **AWS**  | 31               | 99                       | Marktführer, sehr ausgereifte Infrastruktur |
| **Azure**| 60+              | mehrere pro Region       | Starke Hybrid-Cloud & Microsoft-Integration |
| **GCP**  | 38               | 100+                     | Sehr leistungsstarkes Netzwerk (Google) |

---

## ⚙️ 2. Aufgabe: Vergleich eines Dienstes (Compute)

### 🔹 AWS – Amazon EC2
- Virtuelle Maschinen mit voller Kontrolle
- Viele Instanztypen (CPU, RAM, GPU optimiert)
- Skalierung manuell oder automatisch (Auto Scaling)

---

### 🔹 Azure – Azure Virtual Machines
- Ähnlich wie EC2, stark integriert in Microsoft-Umgebung
- Gute Unterstützung für Windows-Server
- Integration mit Azure Active Directory

---

### 🔹 GCP – Compute Engine
- Virtuelle Maschinen mit hoher Performance
- Flexible Preisgestaltung (z.B. automatische Rabatte)
- Sehr schnelle Netzwerk-Infrastruktur

---

## 🔍 Vergleich (Compute-Dienste)

| Kriterium        | AWS EC2                | Azure VM                  | GCP Compute Engine       |
|------------------|----------------------|---------------------------|--------------------------|
| Anbieter         | Amazon               | Microsoft                 | Google                   |
| Fokus            | Flexibilität         | Integration (Microsoft)   | Performance & Daten      |
| Skalierung       | Auto Scaling         | VM Scale Sets             | Managed Instance Groups  |
| Besonderheit     | Marktstandard        | Hybrid-Cloud              | Schnelles Netzwerk       |

---

## 🧠 Fazit

- **AWS** → grösste Auswahl, sehr flexibel  
- **Azure** → ideal für Microsoft-Umgebungen  
- **GCP** → stark bei Performance und Datenanalyse  

Alle drei bieten ähnliche Grunddienste, unterscheiden sich aber in:
- Integration  
- Performance  
- Spezialisierung  

---

## 📌 Ziel erreicht

✔ Infrastruktur verglichen (Regionen & Zonen)  
✔ Compute-Dienste analysiert  
✔ Unterschiede verständlich dokumentiert  
✔ Repository aktualisiert  
