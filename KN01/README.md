# README – Toolumgebung GitLab & Visual Studio Code

## Einführung

In diesem Projekt habe ich eine vollständige und praxisorientierte Toolumgebung für die Arbeit mit GitLab und Visual Studio Code aufgebaut. Ziel war es, eine stabile, sichere und effiziente Entwicklungsumgebung einzurichten, mit der ich meine Projekte lokal entwickeln, versionieren und mit einem Remote-Repository synchronisieren kann. Dabei habe ich sowohl grundlegende als auch weiterführende Konzepte im Bereich Versionskontrolle, SSH-Authentifizierung und Entwicklungsumgebungen angewendet.

## Zusammenfassung

Zu Beginn habe ich sichergestellt, dass mein GitLab-Account korrekt eingerichtet ist. Falls nötig, hätte ich einen neuen Account erstellt, meine E-Mail verifiziert und mein Profil ergänzt. Dies bildet die Grundlage für alle weiteren Schritte, da GitLab als zentrale Plattform für die Versionsverwaltung dient.

Anschliessend habe ich Git (GitBash) auf meinem lokalen Rechner installiert. Nach der Installation habe ich überprüft, ob Git korrekt funktioniert, indem ich Befehle wie `git --version` und `git help` ausgeführt habe. Danach habe ich Git konfiguriert, indem ich meinen Benutzernamen und meine E-Mail global gesetzt habe. Diese Informationen sind wichtig, da sie bei jedem Commit gespeichert werden und die Nachvollziehbarkeit von Änderungen gewährleisten.

Im nächsten Schritt habe ich ein SSH-Keypair erstellt, bestehend aus einem privaten und einem öffentlichen Schlüssel. Den Public Key habe ich in meinem GitLab-Account hinterlegt, während der Private Key sicher auf meinem Rechner bleibt. Zusätzlich habe ich den SSH-Key dem SSH-Agent hinzugefügt und (persistent) konfiguriert, sodass ich mich automatisch authentifizieren kann, ohne jedes Mal mein Passwort eingeben zu müssen. Die Verbindung habe ich mit Befehlen wie `ssh -T git@gitlab.com` erfolgreich getestet.

Danach habe ich ein neues GitLab-Repository erstellt und dieses mit einem lokalen Verzeichnis verknüpft. Ich habe das Repository geklont, die Verbindung überprüft und erste Dateien hinzugefügt. Die vorgegebene README-Vorlage habe ich angepasst und die geforderte Verzeichnisstruktur (KN01–KN05, images, LB2, Reflexion, Quellenverzeichnis) sauber aufgebaut. Anschliessend habe ich die Änderungen mit `git add`, `git commit` und `git push` ins Remote-Repository übertragen und sichergestellt, dass alles korrekt synchronisiert ist.

Zusätzlich habe ich grundlegende Linux-Befehle in der Git Bash angewendet, um mich im Dateisystem zu bewegen und Dateien zu verwalten. Dazu gehören Befehle wie `cd`, `pwd`, `ls`, `mkdir`, `touch`, `cp`, `mv` und `rm`. Durch praktische Übungen konnte ich den Umgang mit der Kommandozeile festigen und effizienter arbeiten.

Zum Abschluss habe ich Visual Studio Code installiert und als zentrale Entwicklungsumgebung eingerichtet. Ich habe wichtige Extensions wie „Markdown All in One“, „Docker“ und „WSL“ installiert, um meinen Workflow zu optimieren. Danach habe ich mein Repository in VS Code geöffnet, Dateien bearbeitet und Änderungen direkt über die integrierte Git-Funktion committet und gepusht. Dadurch konnte ich den gesamten Entwicklungsprozess in einer einzigen Umgebung durchführen.

## Erkenntnisse

Während dieses Projekts habe ich ein besseres Verständnis für Versionskontrolle und moderne Entwicklungsprozesse entwickelt. Besonders wichtig war für mich:

- Die Bedeutung von sauberer Versionsverwaltung mit Git
- Die sichere Authentifizierung mittels SSH-Keys
- Die strukturierte Organisation von Projekten in GitLab
- Der effiziente Umgang mit der Kommandozeile (Bash)
- Die Nutzung von Visual Studio Code als zentrale Entwicklungsumgebung

Ich habe gelernt, wie wichtig es ist, sauber zu arbeiten, Änderungen nachvollziehbar zu dokumentieren und eine klare Struktur im Repository einzuhalten.

## Fazit

Ich bin nun in der Lage, selbstständig mit Git, GitLab und Visual Studio Code zu arbeiten. Ich kann Projekte lokal erstellen, versionieren und mit Remote-Repositories synchronisieren. Zudem kann ich SSH für eine sichere Authentifizierung einsetzen und mich sicher in der Kommandozeile bewegen.

Diese Grundlagen sind essenziell für meine weitere Ausbildung im Bereich Informatik und bilden eine wichtige Basis für zukünftige Projekte und die Zusammenarbeit im Team.
