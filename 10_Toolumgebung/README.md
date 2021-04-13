[**ZURÜCK**](../README.md)


# 10-Toolumgebung

## Inhaltsverzeichnis

* 01 - [GitHub Account](#-git-hub-account)
* 02 - [Git-Client](#git-client)
* 03 - [Repository](#repository)
* 04 - [Vagrant](#vagrant)

## ![](../Bilder_Markdown/githublogo.png "GitHub") Git-Hub Account

**Git-Hub Account erstellen unter:**

[https://github.com/](https://github.com/)

**Neues Projekt starten im Dashboard:**

![Neues Projekt starten](../Bilder_Markdown/NeuesRepositoryerstellen.jpg)

**SSH-Key erstellen**

![SSH Key erstellen](../Bilder_Markdown/SSHKeyerstellen.jpg)

**SSH-Key dem SSH-Agent hinzufügen**

![SSH-Key dem SSH-Agent hinzugügen](../Bilder_Markdown/SSHKeyhinzufuegen.jpg)

Unter dem Feld «Key» muss man den davor kopierten Inhalt der PUB Dateien kopieren.

![Inhalt der Datei kopieren](../Bilder_Markdown/Inhaltrsapubkopieren.jpg)

So sollte es am Ende aussehen.

![SSH-Key nachdem er hinzugefügt wurde](../Bilder_Markdown/SSHKEY.jpg)

 ## ![](../Bilder_Markdown/githublogo.png "GitHub") Git-Client

[**Nach oben**](#10_toolumgebung)

**Installer herunterladen:**

[https://git-scm.com/downloads](https://git-scm.com/downloads)

Während der Installation sollte man beim Wizzard alles beim Standard belassen.

**Git-Client konfigurieren:**

![Git-Client erstellen](../Bilder_Markdown/GitClienterstellen.jpg)

## ![](../Bilder_Markdown/gitbashlogo.jpg "GitClient") Repository

[**Nach oben**](#10_toolumgebung)

**Repository clonen:**

Zuerst muss man die Bash öffnen.

Anschlissend mit folgendem Befehl das Repository clonen:

![Git Repository clonen](../Bilder_Markdown/GitRepositoryclonen.jpg)

In das neue M300-Verzeichnis wechseln, welches man davor erstellt hat:

![Git Bash Verzeichnis wechseln](../Bilder_Markdown/GitVerzeichniswechseln.jpg)

Nun Repository aktualisieren und anzeigen:

![Git Repository aktualisieren und anzeigen](../Bilder_Markdown/GitRepositoryaktualisierenundanzeigen.png)

**Repository herunterladen &amp; aktualisieren (clone/pull):**

**Clone:**

![Git clone](../Bilder_Markdown/Gitclone.jpg)

**Aktualisieren:**

![Git pull](../Bilder_Markdown/Gitpull.jpg)

**Repository hochladen:**

Dateien dem Upload hinzufügen:

![Dateien uploaden](../Bilder_Markdown/Dateiuploaden.jpg)

**Upload commiten:**

![Upload commit](../Bilder_Markdown/Uploadcommit.jpg)

**Und zu guter Letzt Upload pushen:**

![Upload push](../Bilder_Markdown/Uploadpush.jpg)

## ![](../Bilder_Markdown/vagrantlogo.png "GitClient") Vagrant

[**Nach oben**](#10_toolumgebung)

**Vargant installieren unter:**

[https://www.vagrantup.com/](https://www.vagrantup.com/)

**Vagrant File erstellen:**

![Vagrant File erstellen](../Bilder_Markdown/VagrantFileerstellen.jpg)

**Vagrant virtuelle Maschine erstellen:**

![Vagrant VM erstellen](../Bilder_Markdown/VagrantVMerstellen.jpg)

**Verzeichnis der VM wechseln und folgenden Befehl für eine SSH Verbindung mit der VM eingeben:**

![SSH Verbingung zu VM](../Bilder_Markdown/VagrantSSH.jpg)