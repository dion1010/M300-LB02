[**ZURÜCK**](../README.md)

## 30-Container

## Inhaltsverzeichnis 
* 01 - [Container](#container)
* 02 - [Microservices](#microservices)
* 03 - [Docker](#docker)
* 04 - [Beispiele](#beispiele)


## Container
[**Nach oben**](#30-container)

### Was sind Container?

Container kann man wie virtuelle Maschinen sehen, einfach dass diese mehrere Vorteile haben zu normalen KVM Maschinen. Container können den Rollout von Anwendungen beschleunigen und vereinfachen.

Dazu gibt es auch folgende Merkmale:

* Container teilen sich Ressourcen mit dem Host-Betriebssystem
* Container können im Bruchteil einer Sekunde gestartet und gestoppt werden
* Anwendungen, die in Containern laufen, verursachen wenig bis gar keinen Overhead
* Container sind leichtgewichtig, d.h. es können dutzende parallel betrieben werden.
* Container sind "Cloud-ready"!

## Microservices

Microservices sind Architekturkonzepte der Andwendungsentwicklung. Bei Microservices können Services zum Beispiel unabhänging entwickelt und implementiert werden. In anderen Worten gesagt werden bei einer Applikation die Dienste aufgeteilt. So kommt es dann auch dazu, dass diese Dienste verschiedene Programmiersprachen haben können aber schlussendlich sich trozdem verstehen und somit die Applikation auch weiterhin betrieben werden kann.

Denn klassischen Weg der Softwareentwicklung nennt man "monolithischer" Weg.

## Docker
[**Nach oben**](#30-container)

Docker ist eine Weiterentwicklung von der Linux-Containertechnologie. Hauptsächlich besteht die Docker-Plattform aus zwei Komponenten. Einmal dem Docker-Engine (Erstellen & Ausführen von Container) und dem Docker-Hub (Cloud Service für Cointainer Images).

### Docker-Architektur

### Docker Deamon

Man kann sagen, dass der Docker Deamon das Herz von Docker ist. Denn der Docker Deamon beschäftigt sich am meisten mit den Containern. Diese erstellt er, führt er aus und überwacht sie. Dazu baut er auch die Images auf und speichert diese auch.

### Docker Client

Das ClI wird mittels dem Docker Client bedient und die Kommunikation zum Docker Deamon verläuft über HTTP.

### Images

Ein Image ist eine Datei, welche die Umgebung definiert. Wenn man diese starten wird der Container erstellt.
Dazu ist auch wichtig zu Wissen, das ein Image nicht veränderbar ist und nur neu gebuildet werden kann.

### Container

Ist ein ausgeführes Image. Dieses Image kann so oft man will als Containers ausgeführt werden.

### Docker Registry

In dieser Registry werden die Images abgelegt. Standard Registry wie am Anfang beschrieben ist Docker-Hub mit sehr vielen Container-Images. Vorteil von privaten Registries ist einfach, dass man weniger Auslastung hat, da man zum Beispiel jeweils den Download eines Images von der Cloud ausläst.

### Docker Befehle
[**Nach oben**](#30-container)

| Befehl       | Beschreibung                                       | 
| ------------ | -------------------------------------------------- | 
| `docker run`  | Führt ein Befehl in einem neuen Container aus      | 
| `docker start` | Startet einen oder mehrere gestoppte Container     | 
| `docker stop`  | Stoppt einen oder mehrere laufende ontainer        | 
| `docker build` | Erstellt ein Image aus einem Docker-File           | 
| `docker pull`  | Ladet ein Image aus der Registry                   | 
| `docker push`  | Ladet ein Image in die Registry hoch               | 
| `docker exec`  | Führt einen Befehl in einem laufenden Container aus | 
| `docker ps`    | Überblick über aktuelle Container                  |
| `docker images`  | Lokale Images ausgeben | 
| `docker rm`  | Entfernen von einen oder mehreren Container | 
| `docker rmi`  | Löscht ein oder mehrere angegebene Images |  
| `docker kill`  | Fast wie "docker stop" dem  | 

### Dockerfile Hilfe
[**Nach oben**](#30-container)

| Anweisung    | Erklärung 
| ------------ | ----------------------------------------------------------------------------------------- | 
| `FROM` | Gibt an welches "Base" Image verwendet werden soll |
| `ADD` | Kopiert die Datei, aus dem Build Context oder von URLs in das Image| 
| `CMD` | Führt die angegebenen Anweisungen aus, wenn der Container gestartet wurde |
| `COPY` | Kopiert Dateien aus dem Build Context in das Image |
| `ENTRYPOINT` | Legt eine ausführbare Datei fest, welche beim Start des Containers laufen soll |
| `ENV` | Setzt Umgebungsvariablen im Image |
| `HEASLTCHECK` | Docker prüft den Status der Anwendungen in einem Conatainer |
| `MAINTAINER` | Setzt die "Autor-Metadaten" des Image auf den angegebenen Wert |
| `RUN` | Führt die angegebenen Anweisungen im Container aus und bestätigt das Ergebnis |
| `SHELL` | Erlaubt der Shell für folgenden RUN-BEfehk zu setzen. |
| `USER` | Setzt User, welcher in folgeden RUN-, CMD- oder ENTRYPOINT-ANweisungen genutzt werden soll. |
| `VOLUME` | Deklariert die angegebene Datei oder das Verzeichnis als Volumen |
| `WORKDIR` | Setzt Arbeitsverzeichnis für alle folgende RUN-, CMD-, ENTRYPOINT-, ADD oder COPY-Anweisung |

### Docker Volumes 
[**Nach oben**](#30-container)

Falls ein Verzeichnis innerhalb des Containers persistent gespeichert werden soll, muss dies speziell gekennzeichnet werden. 
Dies kann zum Beispiel wichtig sein, wenn man eine MySQL-Datenbank innerhalb eines Containers einsetzt. 

## Beispiele Apache Webserver & Mysql Server
[**Nach oben**](#30-container)

### Build Image:

![Apache Build Image](/Bilder_Markdown/apachebuild.jpg)
![Mysql Build Image](/Bilder_Markdown/mysqlbuild.jpg)

### Container erstellen & starten:

![Apache Run Image](/Bilder_Markdown/apachebuild.jpg)
![Mysql Run Image](/Bilder_Markdown/mysqlrun.jpg)

### Volume erstellen

![presistent Volume](/Bilder_Markdown/presistentvolume.jpg)

Dies kann man dann entweder Im Dockerfile angeben oder mann kann es auch beim run Befehl mit der "-v" Option mitgeben.
Für Beispiel im Dockerfile siehe die Dockerfiles weiter unten.

## Dockerfiles

### Apache Webserver 

```Shell
#Apache Umgebung
#Dion Aziri

FROM ubuntu:14.04
MAINTAINER Dion Aziri

RUN apt-get update

# Apache Installation
RUN apt-get -q -y install apache2 

# Konfiguration Apache
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2

# Übergeordnetes Verzeichnis erstellen
RUN mkdir -p /var/lock/apache2 /var/run/apache2


#phpMyadmin promt-Config
RUN echo 'phpmyadmin phpmyadmin/dbconfig-install boolean true' | debconf-set-selections
RUN echo 'phpmyadmin phpmyadmin/app-password-confirm password lb02dion' | debconf-set-selections
RUN echo 'phpmyadmin phpmyadmin/mysql/admin-pass password lb02dion' | debconf-set-selections
RUN echo 'phpmyadmin phpmyadmin/mysql/app-pass password lb02dion' | debconf-set-selections
RUN echo 'phpmyadmin phpmyadmin/reconfigure-webserver multiselect apache2' | debconf-set-selections


#phpMyadmin Installation
RUN sudo apt-get -y install phpMyadmin

EXPOSE 80

VOLUME /var/www/html

CMD /bin/bash -c "source /etc/apache2/envvars && exec /usr/sbin/apache2 -DFOREGROUND"
```

### Mysql Server

```Shell
#MySQL Umgebung
#Dion Aziri
FROM ubuntu:14.04

MAINTAINER Dion Aziri


#Befehle für mysql-server
RUN echo 'mysql-server mysql-server/root_spassword password lb02dion' | debconf-set-selections 
RUN echo 'mysql-server mysql-server/root_password_again password lb02dion' | debconf-set-selections 

# Installation mysql
RUN apt-get update
RUN apt-get install -y mysql-server


#Port öffnen
RUN sed -i -e"s/^bind-address\s*=\s*127.0.0.1/bind-address = 0.0.0.0/" /etc/mysql/my.cnf


EXPOSE 3306

VOLUME mysql:/var/lib/mysql

CMD ["mysqld"]
```

## Testing

Zugriff auf Webserver testen:

![Apaache Test](/Bilder_Markdown/apachetest.jpg)