# TP2 - Deployment et scaling

On change de méthode, plus un seul pod à la fois, mais 1 fichier de déploiment ```pod-nginx-deployment.yaml``` qui prendra la charge de maintient d'un nombre de pod automatiquement via la template de pod donné:

```yaml
# Version API et kind/type de ressource créée:
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deploy

# Spécifications de la ressource:
spec:
  replicas: 3 # Nombre de pods à maintenir
  selector: 
    matchLabels: # On mettra le label web aux pods créés
      app: web
  
  template: # La template de pods à déployer

    metadata:
      labels:
        app: web # Le label

    spec:
      containers:
        - name: nginx # le nom des pods
          image: nginx:1.27 # L'image des pods
          ports:
            - containerPort: 80 # Le numéro de port ouvert sur le pod

```
On l'apply avec kubectl et on observe la bonne création des 3 pods renseigné ci dessus:

<img src=./images/TP2_image1.png>
<img src=./images/TP2_image2.png>

On peut aussi augmenter le nombre de pod (scaling) manuellement avec la commande suivante qui change le nombre de replicas dans le deployment créé précédemment: 

<img src=./images/TP2_image3.png>

Et on peut changer la version de l'image et revenir en arrière avec les commandes suivantes:

<img src=./images/TP2_image4.png>

<img src=./images/TP2_image5.png>

Dans les deux commandes précédentes on peut observer les actions des nodes sur les pods (suppression et recréation des pods avec ```kubectl get nodes -w```) pour mettre à jour la version de l'image de la template en temps réel.