[**ZURÜCK**](../README.md)

## 40-Kubernetes

## Inhaltsverzeichnis 
* 01 - [Grundbegriffe](#grundbegriffe)
* 02 - [Kubernetes](#kubernetes)
* 03 - [Befehle](#befehle)
* 04 - [Beispiele](#beispiele-yaml-files-für-phpmyadmin-prjekt)
* 
## Grundbegriffe
[**Nach oben**](#40-kubernetes)

### Service Discovery
Dies ist ein Prozess welcher Clients eines Server mit Verbindungsinformation wie zum Beispiel IP und Port versorgt.

Weiter Funktionen_

* Health Checking
* Failover
* Load Balancing
* Verschlüsselung der Daten welche übertragen werden
* Isolieren von Containergruppen

### Lastverteilung (Load Balancing)

Das Load Balancing beschreibt die Verteilung der Last auf mehrere Systeme die untereinander kommunizieren. Als Beispiel dafür kann man einen Webserver nehmen, welcher sehr viele Anfragen bekommt und somit dann auch down gehen kann. Deswegen verteilt man dann die Last.

### Cluster

Ein Cluster ist ein Rechenverbung, oder in anderen Worten gesagt eine Vernetzung von mehreren Computern.

Den Begriff Cluster kann man jedoch auch in Kombination mit zwei anderen Begriffen benutzen:

* HPC-Cluster
  * Erhöhung der Rechenkapazität
* HA-Cluster
  * Erhöhung der Verfügbarkeit

Die Computer in einem Cluster werden auch oft Knoten, Nodes oder Server genannt.

## Kubernetes
[**Nach oben**](#40-kubernetes)

Kubernetes ist ein Open-Source-System welches zur Automatisiereung der Bereitstellung, Skalierung und Verwaltung von Container dient. Kubernetes wird von vielen führenden Cloud-Plattformen unterstütz, wie zum Beispiel Microsoft Azuer oder OpenShift von RedHat.

Merkmale von Kubernetes:

* Unveränderlich
* Ausführung von Anweisungen
* Die Systeme Starten selbst neu nach einem Absturz --> Selbstheilende Systeme
* Loadbalancing

Folgende Objekte gibt es in Kubernetes:

* Pod
  * Ein Pod ist eine Gruppe von Container und Volumes, welche die gleiche Umgebung haben
* ReplicaSet
  * Hier kann man angeben wieviele Replicas dieses Pods hergestellt werden sollten
* Deployment
  * Genauere Angaben zur Konfiguration des Pods
* Service
  * Steuert Zugriff auf Pod
* Ingress
  * ermöglicht Zugriff auf Server über URL
* Secret
  * Erlaubt das speichern von vertraulichen Informationen wie zum Beispiel Kennwörter

## Befehle
[**Nach oben**](#40-kubernetes)

### Apply

Mit apply kann man Ressourcen in einem Cluster erstellen und aktuallisieren.

```Shell
kubectl appl -f PATH_YAML_FILE
```

### Get

Mit get kann man ganz einfach viele Informationen über bestimmte Ressourcen holen.

Zeigt alle Dienste im Namespace auf:

```Shell
kubectl get services
```

Zeigt alle Pods an und deren Status:

```Shell
kubectl get pods
```

Zeigt alle Secret Files an die es gibt.

```Shell
kubectl get secret
```

### Delete

Mit Delete kann man bestimmte Ressourcen löschen.

Im unteren Beispiel sieht man wie man ein pod löschen könnte.

```Shell
kubectl delete pod POD_NAME
```

Mit diesem Befehl kann man auch alles Replicas löschen die in der gleichen Umgebung sind.

```Shell
kubectl delete rs PODNAME_ID
```

## Beispiele YAML Files für phpmyadmin Prjekt
[**Nach oben**](#40-kubernetes)

### mysql Files

### presistent volume (mysql-pv.yaml)
[**Nach oben**](#40-kubernetes)

```Shell
apiVersion: v1
kind: PersistentVolume
metadata:
  name: mysql-pv-volume
  labels:
    app: mysql
spec:
  capacity:
    storage: 2Gi  # allocate the space you want
  volumeMode: Filesystem
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  storageClassName: manual
  hostPath:
    path: /mnt/mysql-data # set the path you want on your machine
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mysql-pv-claim
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 2Gi  # how much is claimed
  storageClassName: manual
```

#### mysql-deployment.yaml
[**Nach oben**](#40-kubernetes)

```Shell
apiVersion: v1
kind: Service
metadata:
  name: mysql
  labels:
    app: mysql
spec:
  ports:
  - port: 3306
    targetPort: 3306
    name: mysql
  selector:
    app: mysql
  type: ClusterIP
---
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: mysql
  name: mysql
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  strategy:
    type: Recreate  # ensure only one instance running
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: mysql
    spec:
      containers:
      - image: mysql:5.6
        name: mysql
        env:
        - name: MYSQL_ROOT_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-secret
              key: root_password
        ports:
        - containerPort: 3306
          name: mysql
        volumeMounts:
        - name: mysql-persistent-storage
          mountPath: /var/lib/mysql
      volumes:
      - name: mysql-persistent-storage
        persistentVolumeClaim:
          claimName: mysql-pv-claim # mount PersistentVolumeClaim here
```

### mysql-secret.yaml
[**Nach oben**](#40-kubernetes)

```Shell
apiVersion: v1
kind: Secret
type: Opaque
metadata:
  creationTimestamp: null
  name: mysql-secret
data:
  root_password: c3VwZXItc2VjcmV0LXBhc3N3b3JkCg==
```

### pma-deployment.yaml
[**Nach oben**](#40-kubernetes)

```Shell
apiVersion: apps/v1
kind: Deployment
metadata:
  name: phpmyadmin-deployment
  labels:
    app: phpmyadmin
spec:
  replicas: 5
  selector:
    matchLabels:
      app: phpmyadmin
  template:
    metadata:
      labels:
        app: phpmyadmin
    spec:
      containers:
        - name: phpmyadmin
          image: bitnami/phpmyadmin
          imagePullPolicy: Always
          ports:
            - containerPort: 80
          env:
            - name: PMA_HOST
              value: mysql-service
            - name: PMA_PORT
              value: "3306"
            - name: MYSQL_ROOT_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: mysql-secrets
                  key: root-password
```

### pma-ingress.yaml
[**Nach oben**](#40-kubernetes)

```Shell
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: phpmyadmin-http-ingress
spec:
  backend:
    serviceName: phpmyadmin-service
    servicePort: 80
```

### pma-service.yaml
[**Nach oben**](#40-kubernetes)

```Shell
apiVersion: v1
kind: Service
metadata:
  name: phpmyadmin-service
spec:
  type: NodePort
  selector:
    app: phpmyadmin
  ports:
  - protocol: TCP
    port: 80
    targetPort: 80
```

### Weiteres Vorgehen
[**Nach oben**](#40-kubernetes)

Alle diese Files muss man natürlich zuerst mit dem Befehl "Apply" aktivieren anschliessend sollte auch schon alles bereit sein und man kann auf das phpmyadmin Webinterface zugreifen.