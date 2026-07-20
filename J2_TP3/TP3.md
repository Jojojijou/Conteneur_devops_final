# TP3 - Self-healing

On peut maintenant tester la persistence du déploiement des pods avec le fichier deployment:

Pour cela on va supprimer un des 5 pods créé après le apply du fichier déploiement: 
<img src=./images/TP3_image1.png>

On peut voir avec un ```kubectl get pods``` que le nombre de pods ne change pas et reste à 5, en effet un autre pod a été créé pour remplacer celui supprimé.