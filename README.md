

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

# Premier composant

* Modifier `index.html`
* Ajouter le composant `src/stock-app.html`

**Vérifier** dans Chrome et IE.

# Compatibilité IE

On ajoute un "polyfill" si le navigateur n'implémente pas les
web component : `webcomponentsjs/webcomponents-lite.min.js`.
Et ça marche sous IE.


# innerHTML

On peut **placer** et **réutiliser** du contenu mis dans un "web component".
Pour cela :

1. mettre du code HTML entre les balises du "web component". Il sera invisible
2. utiliser la balise `<content>` sans et avec selecteur CSS pour l'afficher

# Mise en place d'une liste

* utilisation de `<template is="dom-repeat"></template>` pour générer une boucle : **Ne fonctionne pas pour faiare des tableaux (HTML) avec IE**
* utilisation des annotations
  * binding dans les 2 sens parent vers enfant, enfant vers parent : `{{stocks}}`
  * utilisation dans un seul sens parent vers enfant : `[[items]]`
* définition d'une **propriété** du "web component" typé `Array` et avec une valeur initial `['lait', 'céréals', 'fraises']` (pour le moment).

# Ajout dans la liste

Mettre en place :
* un champ `input type="text"` pour définir un libellé dans le tableau
* un bouton pour ajouter le libellé dans le tableau
* la méthode `_add` qui ajoute un élément à la liste


Mettre en place les tests
```
bower install Polymer/web-component-tester --save
npm install wct --save-dev
```


# Gestion des quantité

* ajout d'un champ quantité pour entrer un produit avec sa quantité
* chargement du stock depuis le local storage au démarage


# Recherche automatique dans la liste

Pour ne pas ajouter 2 fois le même produit, on va chercher dans la liste au fur et à mesure qu'on entre le nom du produit.

Besoin de champ input avancé : au choix `<iron-input>` ou `<paper-input>`. On prend le second car il inclus du **material design**.

On a besoin :
```
bower install PolymerElements/paper-input --save
bower install PolymerElements/paper-button --save
```

On ajoute `filter` et `rendered-item-count` sur le `dom-repeat` pour effectuer des recherches dans la liste.

# Ajout des boutons pour modifier la quantité

* Ajout de 2 boutons pour diminuer ou augmenter la quantité d'un produit.
* Ajout de 2 fonctions pour modififer la quantité du produit.
