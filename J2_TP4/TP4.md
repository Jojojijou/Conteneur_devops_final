# TP4 - Sevice ClusterIP

Dans ce TP, l'objectif est de mettre en place un service ClusterIP avec un fichier ```pod-nginx-service.yaml```:

```yaml
# Service Cluster IP qui va donner une @IP virtuelle partagée entre les pods d'un cluster.
# L'@IP est interne au Cluster et mise automatiquement.
apiVersion: v1
kind: Service # Type de ressource service

metadata:
  name: nginx # Nom de la ressource

spec:
  selector:
    app: web # Pour tous les pods avec le label "web" (défini dans le fichier deployment)

  ports: # On ouvre les ports xxxx : (ici 80 pour http)
    - port: 80
      targetPort: 80
```

On peut apply ce fichier et observer la création du service clusterIP avec les commandes suivantes:

<img src=./images/TP4_image1.png>
<img src=./images/TP4_image2.png>
