le sujet du TP 
lancer le container nexus, deux redirections de port seront nécessaire.
le premier pour accéder à laplateforme devra se faire sur le port 8081 de nexus
le second sera pour que docker puisse se connecter à un registry, j'ai choisi 8084
Pour déployer l'application, il faut allé la containeriser et l'envoyer sur nexus.
ce processus se fait en 4 étapes: 
- docker build #construire l'image contenant l'application.
- docker login #se connecter à nexus.
- docker tag myappimage http://nexus_ip/repository/mydocker/myappimage.
#donner un tag correspondant à l'URL vers l'image à notre image.
- docker push #envoyer l'image sur nexus.
! ATTENTION! vous devrez changer la configuration du docker afin qu'il se connecte
en http, pas en https.Pour ceci, dans le fichier /etc/default/docker ajoutez la ligne 
suivante: DOCKER_OPTS='--insecure-registry NEXUS_IP:NEXUS_REPO_PORT'
si le login ne fonctionne toujours pas, créer un fichier /etc/docker/daemon.json et entrez y ceci:
{
"insecure-registries" :["NEXUS_IP:NEXUS_REPO_PORT"]
}.
