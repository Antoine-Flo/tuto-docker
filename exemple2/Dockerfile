FROM node:alpine

# Créér dossier
WORKDIR /usr/src/app

# Copier fichiers .json puis installer dépendance
COPY package*.json ./
RUN npm install


# Bundle app source
COPY . .

EXPOSE 3000
CMD [ "node", "app.js" ]
