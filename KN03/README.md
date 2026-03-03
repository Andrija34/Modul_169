# 🚀 Teil 1 / AWS EC2 mit Infrastructure as Code (IaC) – Learner Lab

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

## Instanz starten

EC2-Instanz in AWS starten und warten, bis der Status **running** ist.

---

## SSH-Zugriff

### Speicherort Private Key (Windows Beispiel)
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



# Teil 2 / OCI-Images, Container und Registry – BASICS

## Ausgangslage

Moderne Softwareentwicklung erfordert flexible und portable Lösungen, um Anwendungen unabhängig von der Umgebung lauffähig zu machen. Klassische Installationen sind oft fehleranfällig, da sie von der spezifischen Systemkonfiguration abhängen.

Docker, Podman und ähnliche Tools lösen dieses Problem, indem sie Anwendungen und alle benötigten Abhängigkeiten in **Containern** verpacken. Dadurch laufen sie zuverlässig auf unterschiedlichen Systemen – egal ob Laptop, Server oder Cloud.

📌 In diesem Challenge geht es um die **Basic-Konzepte und Commands** rund um OCI-Images, Container und Registries. Es werden noch keine eigenen Images erstellt (kein Dockerfile, kein eigener Code).

---

# Warum starten wir mit Docker?

Docker ist:

- Industriestandard
- Weit verbreitet
- Gut dokumentiert
- Große Community
- Viele Tutorials und Beispiele

Podman wird später behandelt.

---

# Unterschied Docker vs. Podman

Docker:
- Benötigt zentralen Daemon (dockerd)
- Läuft meist mit Root-Rechten
- Sehr verbreitet im Enterprise-Bereich

Podman:
- Kein zentraler Daemon
- Arbeitet nutzerbasiert
- Unterstützt rootless Mode
- Höhere Sicherheit

---

# OCI-Images und Container

Ein OCI-Image ist eine Vorlage (Bauplan).  
Ein Container ist die laufende Instanz dieses Images.

## Vergleich mit Postpaketen

OCI-Image = Verpackung mit Smartphone + Zubehör  
Container = Das ausgepackte, laufende Smartphone  
Registry = Lager mit allen Paketen (z.B. Docker Hub)

---

# Wichtige Begriffe

Registry  
Online-Speicher für Images (Docker Hub, GitLab Registry)

Docker-Daemon  
Hintergrunddienst zur Verwaltung von Containern

Docker-Client  
CLI-Tool zur Kommunikation mit Docker (z.B. docker ps)

OCI-Image  
Bauplan für Container

Image vs. Container  
Image = Vorlage  
Container = Laufende Instanz

---

# Basic Docker Commands

## docker run

Startet einen neuen Container.

Test:
```bash
docker run hello-world

Interaktive Shell:

docker run -it ubuntu /bin/bash

Detached Mode:

docker run -d ubuntu sleep 20

Container automatisch löschen:

docker run -d --rm ubuntu sleep 20
docker ps

Aktive Container:

docker ps

Alle Container:

docker ps -a

Nur IDs:

docker ps -a -q
docker images

Lokale Images anzeigen:

docker images

Alternative:

docker image ls
Container und Images löschen

Container löschen:

docker rm <NAME>

Image löschen:

docker rmi ubuntu
Container starten

Gestoppten Container starten:

docker start <ID>
Container stoppen / killen

Sauber stoppen:

docker stop <ID>

Sofort beenden:

docker kill <ID>
Informationen zu Containern

Logs anzeigen:

docker logs <ID>

Details anzeigen:

docker inspect <ID>

Änderungen anzeigen:

docker diff <ID>

Prozesse anzeigen:

docker top <ID>
🟢 2. Teil-Challenge
SSH-Verbindung zur EC2
ssh -i M169.pem ubuntu@<Public-IP>
Docker überprüfen
docker info
docker --version
Erste Docker-Befehle

Images anzeigen:

docker image ls

Laufende Container:

docker ps

Image aus Registry laden:

docker pull hello-world

Container starten:

docker run hello-world

Container stoppen und löschen:

docker stop <ID>
docker rm <ID>
Sonder-Challenge – NGINX Webserver

Container starten:

docker run -d -p 8080:80 nginx

Browser öffnen:

http://<Public-IP>:8080

Falls kein Zugriff:

Security Group um Port 8080 erweitern

Überprüfung:

docker container ls
docker image ls

Ergebnis:
NGINX Standard-Webseite sichtbar

Ziel der Übung

Grundbegriffe verstehen

Unterschied Image vs. Container kennen

Registry verstehen

Docker-Befehle ausführen können

Container isoliert erklären können

Teil-Leistungsnachweis

✔ docker run, docker ps, docker stop ausführen
✔ Container starten und Status prüfen
✔ Unterschied Container vs. VM erklären
✔ Isolation von Containern erklären

Fachgespräch

Image vs. Container erklären
Bedeutung von Docker Hub erklären
Vorteile isolierter Container erklären
Bonus: nginx-Webserver live demonstrieren



# 🐳 Teil 3 /  OCI-Images mit Docker – RUN & ADMINISTRATION

## Ausgangslage

Container-Technologien wie Docker ermöglichen es, Anwendungen isoliert auszuführen. Zwei zentrale Konzepte spielen dabei eine wichtige Rolle:

- **Networking**
- **Volumes**

Diese Konzepte erlauben:
- Zugriff von außen auf Container
- Persistente Datenspeicherung über den Container-Lebenszyklus hinaus

---

# Container Networking

Wenn ein Webserver in einem Container läuft, muss dieser über **Ports** erreichbar gemacht werden.

Dies geschieht mit:

- `-p` → explizite Portweiterleitung
- `-P` → automatische Portzuweisung

## Beispiele

MySQL Container an Host-Port 3306 binden:

```bash
docker run --rm -d -p 3306:3306 mysql

Automatische Portvergabe:

docker run --rm -d -P mysql
Dockerfile – Ports freigeben

Ports werden im Dockerfile mit EXPOSE definiert:

EXPOSE 3306
Netzwerkmodi

Bridge (Standard)
None (keine Netzwerkschnittstelle)
Host (nutzt Host-Netzwerk direkt)

Zusätzlich: Benutzerdefinierte Netzwerke möglich

Container Volumes

Container verlieren ihre Daten beim Löschen.
Volumes ermöglichen persistente Speicherung.

Vorteile von Volumes

Daten bleiben nach Container-Löschung erhalten

Mehrere Container können Daten teilen

Performance-optimiert

Unabhängig vom Container-Lebenszyklus

Docker löscht Volumes nie automatisch

Beispiel Volume-Mount

MySQL-Datenverzeichnis auf Host einhängen:

docker run -d -p 3306:3306 -v ~/data/mysql:/var/lib/mysql --name mysql --rm mysql

Dateien prüfen:

ls -l ~/data/mysql
Hands-on Lab – MariaDB mit Docker

Ziel:
MariaDB in einem Container betreiben und persistent speichern.

Lernziele

Container starten, stoppen, löschen

Verbindung mit HeidiSQL herstellen

Port-Forwarding einrichten

Persistente Speicherung mit Volumes

Troubleshooting durchführen

Ablauf
Schritt 1 – Vorbereitung

HeidiSQL installieren

Docker Images prüfen

MariaDB-Image laden

Container starten

Schritt 2 – Container verwalten

Container stoppen

Container starten

Container löschen

Security Group ggf. anpassen

Schritt 3 – Datenbank erstellen

Verbindung via HeidiSQL herstellen

Datenbank erstellen:

M169_KN03_XXX

(XXX = erste drei Buchstaben des Nachnamens)

Schritt 4 – Datenpersistenz testen

Volume einrichten

Container löschen

Container neu erstellen

Prüfen, ob Datenbank weiterhin existiert

Ziel der Übung

MariaDB läuft im Container

Zugriff via HeidiSQL möglich

Port-Forwarding funktioniert

Daten bleiben persistent gespeichert

Volumes korrekt eingesetzt

3. Teil-Leistungsnachweis

✔ Verbindung via HeidiSQL möglich (Live-Demo)
✔ Wechsel in laufenden Container möglich
✔ Begriff „Persistent“ erklären können
✔ Container löschen & neu erstellen ohne Datenverlust
✔ Dokumentation im Repo mit Screenshots vorhanden
