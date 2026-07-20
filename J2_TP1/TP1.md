# TP1 - Premier pod nginx:

On crée le fichier ```pod-nginx.yaml``` qui servira à créer 1 simple pod avec l'image nginx:

``` yaml
apiVersion: v1
kind: Pod
metadata:
  name: mon-nginx
  labels:
    app: web
    
spec:
  containers:
    - name: nginx
      image: nginx:1.27
      ports:
        - containerPort: 80
```

Puis on le déploye avec ```kubectl apply -f <nom_du_fichier>``` et on observe sa création avec ```kubectl get pods```:

<img src=./images/TP1_image1.png>

La commande describe va servir à obtenir plus d'informations sur le noeud, et la commande exec va permettre d'executer diverses commandes sur le noeud (ici lancer un environnement shell): 

<img src=./images/TP1_image2.png>

