[**ZURÜCK**](../README.md)

## 30-Container

## Inhaltsverzeichnis 
* 01 - [Container](#container)
* 02 - [Microservices](#microservices)
* 03 - [Docker](#docker)
* 04 - [Kubernetes](#kubernetes)
* 05 - [Sicherheitsaspekte](#sicherheitsaspekte)
* 06 - [Netzwerkplan](#netzwerkplan)
* 07 - [Testing](#testing)

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

In dieser Registry werden die Images abgelegt.

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
| `docker exec`  | Führ einen Befehl in einem laufenden Container aus | 

### Docker Volumes 
[**Nach oben**](#30-container)

Falls ein Verzeichnis innerhalb des Containers persistent gespeichert werden soll, muss dies speziell gekennzeichnet werden. Dies kann zum Beispiel wichtig sein, wenn man eine MySQL-Datenbank innerhalb eines Containers einsetzt. 

## Kubernetes
[**Nach oben**](#30-container)



## Sicherheitsaspekte
[**Nach oben**](#30-container)



## Netzwerkplan
[**Nach oben**](#30-container)



## Testing
[**Nach oben**](#30-container)

