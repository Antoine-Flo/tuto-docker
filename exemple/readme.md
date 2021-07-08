# Exemple 1
1. Créer l'app express

```js
const express = require('express')
const app = express()
const port = 8080

app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(port, () => {
  console.log(`App listening port ${port}`)
})
```

1. Créer Dockerfile
```dockerfile
FROM node:alpine

# Créer dossier app
WORKDIR /usr/src/app

# Copier fichiers .json [source destination]
COPY package*.json ./

# Installer dépendance
RUN npm install

# Copie l'app dans le nouveau dossier
COPY . .

# Ouvre le port 3000 du container
EXPOSE 3000
CMD [ "node", "app.js" ]
```

3. Créer .dockerignore

```
node_modules
```

4. Executer les commandes

```
docker build . -t linstantcode/test-app
docker run -p 3000:3000 -d linstantcode/test-app
```


5. Se connecter :
`http://localhost:3000/`