# TP5 - Service NodePort

Le service NodePort va permettre d'exposer un port sur tous les pods d'un cluster. Dans ce TP on va exposer le port 30080 qui va rediriger vers le port 80 avec le fichier ```pod-nginx-service-nodeport.yaml```:

```yaml
apiVersion: v1
kind: Service # Type de ressource service

metadata:
  name: nginx # Nom de la ressource

spec:
  type: NodePort
  selector:
    app: web # Pour tous les pods avec le label "web" (défini dans le fichier deployment)

  ports: # On ouvre les ports xxxx : (ici 30080 qui redirigera vers 80 pour http)
    - port: 80
      targetPort: 80
      nodePort: 30080
```

On peut l'appliquer et contacter un des nodes contenant les pods nginx:

<img src=./images/TP5_image1.png>
<img src=./images/TP5_image2.png>

(Note: On contacte le noeud sur le port 8080 car on a fait une redirection forward port vers le port 8080 du noeud pour pouvoir le contacter)
