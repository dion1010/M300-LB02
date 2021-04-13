## 30-Container

## Inhaltsverzeichnis 

* 01 - [Docker](#docker)
* 02 - [Kubernetes](/20_Infrastruktur_automatisierung)
* 03 - [30-Container](/30_Container/README.md)
* 04 - [Persönlicher Wissensstand](#persönlicher-wissenstand)
* 05 - [Schlusswort](#schlusswort)

-   01 - Einstieg 

-   02 - Docker / Kubernetes Umsetzung 

-   03 - Sicherheitsaspekte 

-   04 - Abschluss 

### Docker

 
### Docker Befehle
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

Falls ein Verzeichnis innerhalb des Containers persistent gespeichert werden soll, muss dies speziell gekennzeichnet werden. Dies kann zum Beispiel wichtig sein, wenn man eine MySQL-Datenbank innerhalb eines Containers einsetzt. 


### Netzwerkplan 

    +---------------------------------------------------------------+ 
    ! Container: Nginx Frontend Webserver - 34.65.185.255:80        ! 

    ! Container: Python Flask Backend API - 34.65.90.233:8080       ! 

    ! Container: MySQL Datenbank - Hostname: mysql - no public IP   ! 
    +---------------------------------------------------------------+ 
    ! Container-Engine: Docker                                      ! 
    +---------------------------------------------------------------+ 
    ! Kubernetes Umgebung Google Cloud (GKE) - 3 Node Cluster       ! 
    +---------------------------------------------------------------+ 
    ! Notebook macOS - Schulnetz 10.x.x.x                           ! 
    +---------------------------------------------------------------+ 

 

 

### Relevante Befehle 

 

-   docker build -t fnoah/m300-lb02-web . 

-   docker push fnoah/m300-lb02-web 


-   delete pod to update image 

 

-   kubectl expose deployment hello-minikube --type=NodePort 

 

-   kubectl exec -it web-deployment -- /bin/bash 

 

-   kubectl get services 