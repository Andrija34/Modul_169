# 🚀 AWS EC2 mit Infrastructure as Code (IaC) – Learner Lab

## Ausgangslage

Infrastructure-as-Code (IaC) ist ein Ansatz zur automatisierten Bereitstellung und Verwaltung von IT-Infrastrukturen über Code. Anstatt manuell eine Instanz zu konfigurieren, wird ein vordefiniertes Skript verwendet, um eine AWS EC2-Instanz bereitzustellen. Dies sorgt für eine konsistente Umgebung und reduziert menschliche Fehler.  

In diesem Workshop wird eine Ubuntu-basierte Instanz mit vorinstalliertem Docker und Podman aufgesetzt, die für Container-Labs genutzt wird.

---

# Schritt 1: AWS Academy Learner Lab starten

1. AWS Academy Website öffnen  
2. Auf **Student Login** klicken  
3. Mit AWS Academy Konto anmelden  
4. Im Dashboard auf **Learner Lab** klicken  
5. Unter Modules das Learner Lab starten (Launch)  
6. Auf **Start Lab** klicken  
7. Warten bis der Status neben AWS grün 🟢 ist  
8. AWS Management Console öffnen  

Nach Abschluss:  
- **Stop Lab** klicken, um Ressourcen zu pausieren  
- Erstellte EC2-Instanzen bleiben bestehen  

---

# Schritt 2: EC2-Instanz erstellen

## Basis-Konfiguration

- Name: `M169-Lab`  
- AMI: Neuestes Ubuntu Server Image  
- Instance Type: `t3.micro`  
- Key Pair: Erstellen oder auswählen (für SSH-Zugriff)  
- Network: Default VPC  

---

## Security Group – Inbound Rules

| Typ              | Protokoll | Port | Source       | Beschreibung |
|------------------|-----------|------|-------------|-------------|
| SSH              | TCP       | 22   | 0.0.0.0/0   | SSH Zugriff |
| HTTP             | TCP       | 80   | 0.0.0.0/0   | Web Zugriff |
| Custom TCP       | TCP       | 5000 | 0.0.0.0/0   | Port 5000 Forwarding |
| Custom TCP       | TCP       | 5001 | 0.0.0.0/0   | Port 5001 Forwarding |
| All ICMP - IPv4  | ICMP      | All  | 0.0.0.0/0   | Ping |

---

# cloud-init Script (IaC)

Unter **Advanced Details → User Data** folgendes Script einfügen:

```yaml
#cloud-config

packages:
  - apt-transport-https
  - ca-certificates
  - curl
  - gnupg-agent
  - software-properties-common

write_files:
  - path: /etc/sysctl.d/enabled_ipv4_forwarding.conf
    content: |
      net.ipv4.conf.all.forwarding=1

groups:
  - docker

runcmd:
  - curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
  - add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
  - apt-get update -y
  - apt-get install -y docker-ce docker-ce-cli containerd.io
  - systemctl start docker
  - systemctl enable docker
  - apt-get install podman -y
  - systemctl start podman
  - systemctl enable podman
  - usermod -aG docker ubuntu
```
Instanz starten.

SSH-Zugriff
Speicherort Private Key

Windows Beispiel:
```
C:\Users\<Benutzer>\.ssh\
```
Verbindung herstellen
chmod 400 M169.pem
ssh -i M169.pem ubuntu@<Public-IP>
Installation überprüfen
Docker prüfen
docker --version
systemctl status docker

Erwartet:

Versionsnummer sichtbar

Status: active (running)

Podman prüfen
podman --version
systemctl status podman

Erwartet:

Versionsnummer sichtbar

Status: inactive (dead) → korrektes Verhalten

Unterschied Docker vs. Podman
Docker

Benötigt Daemon (dockerd)

Läuft mit Root-Rechten

Zentrale Container-Verwaltung

Weit verbreitet

Podman

Kein Daemon erforderlich

Unterstützt rootless Mode

Container laufen als User-Prozess

Höhere Sicherheit

Warum ist Podman „inactive“?

Podman läuft on-demand:

Kein permanenter Hintergrunddienst

Container starten direkt als Benutzerprozess

Ressourcenschonend

Sicherheitsvorteil durch rootless Betrieb

Das Verhalten inactive (dead) ist normal.

Vorteile von Infrastructure as Code

Automatisierte Bereitstellung

Wiederholbare Konfiguration

Reduktion menschlicher Fehler

Schnellere Deployments

Versionierbar (Git)

Konsistente Umgebungen

Leistungsnachweis

✔ EC2-Instanz via IaC erstellt
✔ SSH-Zugriff funktioniert
✔ Docker installiert und aktiv
✔ Podman installiert
✔ Unterschied Docker vs. Podman verstanden
✔ Repository vollständig dokumentiert
