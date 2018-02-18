

# Objectif

Etude de cas d'une application de gestion de stock
avec Polymer 1.x.

On utilisera `bower` avec la version 1.x de Poluymer.


# Mise en place

1. Créer le dossier
2. Initialiser git
3. Installer bower si besoin : `npm install -v bower`
4. Initialiser le projet bower : `bower init`
4. Installer Polymer 1.x ` bower  install Polymer/polymer#^1.x --save`

# Première page avec Server

## On install le server
```
npm init
npm install static-server --save-dev
```
## Server

```javascript
var StaticServer = require('static-server');
var server = new StaticServer({
  rootPath: '.',            // required, the root of the server file tree
  name: 'my-http-server',   // optional, will set "X-Powered-by" HTTP header
  port: 8080,               // optional, defaults to a random port
  host: 'localhost',       // optional, defaults to any interface
  cors: '*',                // optional, defaults to undefined
  templates: {
    index: 'index.html',      // optional, defaults to 'index.html'
    notFound: '404.html'    // optional, defaults to undefined
  }
});
server.start(function () {
 console.log('Server listening to', server.port);
});

```

## index.html

Faire un simple "Hello World".
