# **Tutoriel Docker**
👋 Bienvenue sur ce tutoriel à la découverte de Docker.
Retrouver [la vidéo sur la chaîne.]()

***
## 📖 **Définitions**

<ins>Image</ins> : Modéle à partir duquel sera créé un ou des containers.<br>

<ins>Container</ins> : *Processus et toute ses dépendances, isolés, en cours d'execution.*<br>

<ins>Docker file</ins> : *Liste de commandes pour créer une image*<br>


<ins>Bind-Mount</ins> : *Fait pointé un fichier ou dossier du container vers un fichier ou dossier de l'hôte, vers l'extérieur du container.*


***
## 💻 **Commandes**

### Naviguer
```js
docker 
// Liste les commandes et les familles de commande

docker system info
// Affiche information au sujet du système

docker image ls 
// Liste les images (ou 'docker images')

docker container -a ls 
// Liste les containers (même inactif).
```

### Executer
```js
docker pull hello-world
// Télécharge image depuis docker-hub

docker run hello-world
// Démarre processus dans container 

docker run -it ubuntu bash
// Télécharge et lance ubuntu, execute bash interactif
```

### Supprimer
```js
docker rm [container id]
// Supprime container

docker rmi [image name]
// Supprime image

docker system prune
// Supprime espace inutilisé
```

***
## 📁 **Dockerfile**
### Etapes
1. Créer fichier Dockerfile
1. Décrire étape de création de l'image (utiliser référence)
1. `docker build .`

### Référence
```dockerfile
FROM ubuntu:18.04
# image de base

LABEL my.image.version="0.0.1"
# Donner un nom à votre image

RUN npm install
# Exécuter commandes

COPY . /app
# Copie fichiers locaux dans container. Source | Destination

VOLUME ["/data"]
# Espace de stockage amener à être modifier (mount point)

EXPOSE 80
# Quel port du container doit être ouvert

ENV MY_VAR="Example" 
# Variable d'environnement

ENTRYPOINT ["cmd", "param1", "param2"]
# Commande principale

CMD 
# Commande optionnel

WORKDIR
```