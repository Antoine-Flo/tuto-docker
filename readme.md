# **Tutoriel Docker**
👋 Bienvenue sur ce tutoriel à la découverte de Docker.
Retrouvez [la vidéo sur la chaîne.]()

***
## 📖 **Définitions**

<ins>Image</ins> : *Modéle à partir duquel sera créé un ou des containers.*<br>

<ins>Container</ins> : *Processus et toute ses dépendances virtuellement isolé*<br>

<ins>Docker file</ins> : *Liste de commandes pour créer une image (voir section Dockerfile).*<br>

<ins>Docker deamon</ins> : *Processus Docker en arrière plan qui gère images et containers.*<br>

<ins>Registry</ins> : *Lieu d'échange et de stockage d'images (exemple : Docker Hub).*

<ins>Bind-Mount</ins> : *Fait pointé un fichier ou dossier du container vers un fichier ou dossier de l'hôte, vers l'extérieur du container.*


***
## 💻 **Commandes**

### Structure d'une commande
```
docker <catégorie> <commande> <options>
```
### Naviguer
```js
docker 
// Liste les commandes et les familles de commande

docker system info
// Affiche informations au sujet du système

docker image ls 
// Liste les images (ou 'docker images')

docker image history myImage:0.0.0
// Voir les différents étages de l'image

docker container -a ls 
// Liste les containers, même inactif (ou 'docker ps -a')
```

### Executer
```js
docker pull hello-world
// Télécharge image depuis docker-hub

docker create hello-world
// Crée un container depuis une image

docker start myContainer
// Démarre un container arrêté

docker run hello-world
// Raccourci 'docker create' && 'docker start' avec tag -t

docker exec 
// Executer une commande

docker run -it --rm ubuntu bash
// Télécharge et lance ubuntu, execute bash interactif, supprime container aprés exécution
// -it = --interactive + --tty
```

### Volume
```js
docker volume create myvolume
// Crée un espace de stockage
```

### Arrêter / Supprimer
```js
docker container stop myContainer
// Arrête container

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
1. Créer fichier `Dockerfile` & `.dockerignore`
1. Décrire étape de création de l'image (utiliser référence)
1. `docker build -t myname/firstimage:0.1 .`

### Référence
```dockerfile
FROM ubuntu:18.04
# image de base

LABEL my.image.version="0.0.1"
# Donner un nom à votre image

RUN npm install
# Exécuter commandes

WORKDIR /usr/src/app
# Crée dossier si n'existe pas, cd dedans

COPY . /app
# Copie fichiers locaux dans container. Source | Destination

VOLUME ["/data"]
# Espace de stockage amener à être modifier (mount point)

EXPOSE 80
# Quel port du container doit être ouvert

ENV MY_VAR="Example" 
# Variable d'environnement

ENTRYPOINT ["cmd", "param1", "param2"]
# Commande principale, mode exec, démarre pas shell

CMD 
# Commande optionnel
```

## 🕸 **docker-compose**
### Etapes
1. Créer fichier `docker-compose-yaml`
1. Décrire étape de création du setup
1. `docker-compose up`

### Référence
```yaml
version: "3.9"  # optional since v1.27.0
services:
  web:
    build: .
    ports:
      - "5000:5000"
    volumes:
      - .:/code
      - logvolume01:/var/log
    links:
      - redis
  redis:
    image: redis
volumes:
  logvolume01: {}
```