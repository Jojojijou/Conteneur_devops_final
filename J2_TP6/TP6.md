# TP6 - Projet: MySQL + phpMyAdmin sur K8s

Le but de ce TP sera de faire tourner 4 pods: Il y aura 1 pod avec mysql et 3 pods avec phpMyAdmin. Le tout sera déployé via deux fichiers deployment, avec une clusterIP pour le pod mysql et un nodePort pour les pods phpMyAdmin.

Voici les deux fichiers deployments ```mysql-deployment.yaml``` et ```php-deployment.yaml``` semblables à celui que nous avons fait pour nginx:

* *mysql-deployment.yaml*:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql-deploy

spec:
  replicas: 1 # 1 seul noeud mysql à créer et à maintenir
  selector: 
    matchLabels: 
      app: mysql
  
  template: 

    metadata:
      labels:
        app: mysql

    spec:
      containers:
        - name: mysql
          image: mysql:8 
          ports:
            - containerPort: 3306 
            
          env: # Mise en place de variable d'environnement pour mysql sur le pod non sécurisé pour le moment
          - name: MYSQL_ROOT_PASSWORD
            value: "rootroot"
```

* *php-deployment.yaml*: 
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: php-deploy

spec:
  replicas: 2 # 2 noeuds PhpMyAdmin à créer et à maintenir au minimum
  selector: 
    matchLabels: 
      app: php
  
  template: 

    metadata:
      labels:
        app: php

    spec:
      containers:
        - name: php 
          image: phpmyadmin:latest 
          ports:
            - containerPort: 3306 
          
          env: 
          - name: PMA_ARBITRARY
            value: "1"
```
On apply ces deux fichiers:

* *mysql-deployment.yaml*:
<img src=./images/TP6_image1.png>
<img src=./images/TP6_image2.png>

* *php-deployment.yaml*: 
<img src=./images/TP6_image3.png>
<img src=./images/TP6_image4.png>

Ensuite on crée et on applique les deux fichiers ```mysql-service.yaml``` et ```php-service.yaml``` qui contiendront respectivement la clusterIP pour mysql et le nodePort pour phpMyAdmin:

* *mysql-service.yaml*:
```yaml
apiVersion: v1
kind: Service

metadata:
  name: mysql

spec:
  selector:
    app: mysql

  ports:
    - port: 3306
      targetPort: 3306
```

* *php-service-nodeport.yaml*:
```yaml
apiVersion: v1
kind: Service

metadata:
  name: php-nodeport 

spec:
  type: NodePort
  selector:
    app: php 

  ports:
    - port: 80
      targetPort: 80
      nodePort: 30080
```

<img src=./images/TP6_image5.png>
<img src=./images/TP6_image6.png>

On contacte bien phpMyAdmin.
