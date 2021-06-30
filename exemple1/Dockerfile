FROM node:alpine

# Créér dossier
WORKDIR /usr/src/app

# Copier fichiers .json puis installer dépendance
COPY package*.json ./
RUN npm install && npm cache clean --force


# Bundle app source
COPY . .

EXPOSE 3000
CMD [ "node", "app.js" ]
