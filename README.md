# Developer documentation

# Sommaire

 * ### Intégration

   + [BEM](#bem) 
   + [Pseudos Attributs](#attributs)
   + [Unités](#unites)
   + [FlexboxGrid](#flexbox)
   + [Grid Layout](#grid)
   + [SCSS](#scss)
   + [Mixins](#mixins)
   + [CSS Tips](#tips)
   + [Font-face](#font-face)

* ### Javascript

  + [Conditions & Boucles](#conditions&Boucles)
  + [Tableaux & Dictionnaires](#tableaux&Dictionnaires)
  + [Ajax](#ajax)


## Intégration

<a id ="bem"><a>

* -> __Block__
* -> __Element__
* -> __Modifier__

BEM apporte également une convention de nommage des classes CSS. Ce qui compose un page ou une application Web peut toujours être rangé dans une arborescence de blocs, d'éléments et de modificateurs.

__Bloc__

Un bloc est une entité indépendante, une « brique » de l'application ou de la page Web. Un bloc forme son propre contexte autonome.

__Element__

Un élément est une partie d'un bloc.

__Modifier__

Un modificateur est une propriété qui sert à créer des variantes, pour faire des modifications minimes comme changer des couleurs. Il existe des modificateurs de blocs et des modificateurs d'éléments.

-> _La méthodologie BEM établit ensuite trois règles essentielles :_

* Les blocs et les éléments doivent chacun avoir un nom unique, lequel sera utilisé comme classe CSS
</br>
</br>

* Les sélecteurs CSS ne doivent pas utiliser les noms des éléments HTML (pas de .menu td) ;
</br>
</br>

```html

block-name
block-name_modifier_name
block-name__element-name
block-name__element-name_modifier_name

```

```html

<div class="search-box search-box_light">
  <!-- (input field here) -->
  <button class="search-box__btn search-box__btn_max_visible">Search</button>
</div>

```

```css

.search-box {
  height: 300px;
  width: 300px;
}
.search-box_light {
  background-color: #DEF;
  color: #777;
}
.search-box__btn {
  padding: 4px;
}
.search-box__btn_max_visible {
  font-weight: bold;
}

```


## Pseudo attribut :: after & :: before <a id ="attributs"><a>

### Attention
* Il est obligatoire d'avoir un `content:''` afin que vos after/ before s'affichent.
* Vous pouvez leur donner une taille, une position (absolute par rapport à son parent)
* Essentiellement utilisé pour de la décoration

```html

<section class="cover">
<h2 class="cover__title">Présentation</h2>
</section>
```

```css

Si je veux des ornements en haut et a gauche d'un titre

.cover{
&__title{
  font-size: 24px;
  color: #bbb;
  text-align: center;
  position: relative;
  &::before,
  &::after{
    content:'';
    position: absolute;
    top:0;
    display: block;
    width: 50px;
    height: 50px;
    background: green;
  }
  &::before{
    left: 0;
  }
  &::after{
    right: 0;
  }
}
}

```

## Les unités <a id ="unites"><a>


### REM

L'unité de mesure REM est basée sur la taille de l'élément racine du HTML.
Par défaut, la taille du <html> est de 16px, ce qui veut dire que `1rem = 16px`.
Pour éviter de devoir faire des calculs afin de respecter les tailles relatives à votre maquette,
vous pouvez ré-écrire cette `font-size`afin que `1rem = 10px`

Les proportions et tailles vont s'adapter à la taille de l'écran en cas de zoom, ce qui est impossible en px.

```css

html{
/*
override de la valeur par défaut
afin que 1rem = 10px;
*/
font-size: 62.5%; (passage de 16px a 10 pixel)
}

.mainTitle{
font-size: 2.4rem; (24 pixel)
}

.cover{
width: 32rem; (320 pixel)
}

```

### EM

Le `EM` à contrario du `REM`se base quant à lui sur la taille de son parent direct. (pas son grand-parent). </br>
Cette unité représente la font-size calculée de l'élément. Si utilisée avec la propriété font-size, elle représente la taille de police héritée de l'élément.

```css

html{
font-size: 100%;
}

.cover{
height: 100px;
&-title{
  font-size: .8em;
}
&-subTitle{
  font-size: .6em;
}
}
```
### VW(width)/ VH(heigth) Sizing (unités) / vmin

Ces unités permettent entre autres d'avoir une taille de police et des colonnes variables selon la résolution de l'écran. Lors de la réduction du corps de la fenêtre votre titre se réduira suivant le schéma initialement prévu.

Les valeurs utilisées peuvent être quelque peu déroutantes si vous n'avez pas utilisé ces unités avant. 1VH représente 1% de la fenêtre courante (la zone de contenu de la fenêtre du navigateur) de hauteur, au lieu de 100% comme vous pouvez vous y attendre.

Donc si vous voulez un élément à la hauteur de votre fenêtre, vous devrez le mettre à 100vh. Bien sûr VW fonctionne exactement de la même manière que les unités de VH.

En résumé:

1vw = 1% de la largeur de la fenêtre

1VH = 1% de la hauteur de la fenêtre

1vmin = 1vw ou 1VH, soit la valeur la plus petite

1vmax = 1vw ou 1VH, soit la valeur la plus grande


section {

    height: 80vh;

    width: 80vw;

}



### Les grilles avec FlexboxGrid <a id ="flexbox"><a>

Documentation (http://FlexboxGrid.com/)

Il ne faut pas confondre FlexboxGrid et CSS grid. Le nombre maximum de colonne est de 12. Ces grilles permettent de se repéré sur Sketch. Dans une ligne on peut déclaré autant de colonne que l'on veux. Il existe deux types de container le classique (container) et le fluid. Les 12 colonnes prennent la taille du container.
Il est possible de faire des grilles dans des grilles (Nested Grids = voir site FlexboxGrid).
On peut également ajouter des offset : permet de dire au colonne de commencer a partir de la colonne que l'on veux. On décale ainsi de deux colonnes.


Taille :

xs = mobile </br>
sm = small (petite tablette) </br>
md = medium ( tablette ) </br>
lg = large ( desktop) </br>
row= lignes </br>
col= colonnes


```HTML
<div class="container">

<div class="row">

  <div class="col-xs-12 col-md-6 col-lg-3"></div>
  <div class="col-xs-12 col-md-6 col-lg-3"></div>
  <div class="col-xs-12 col-md-6 col-lg-3"></div>
  <div class="col-xs-12 col-md-6 col-lg-3"></div>
  <div class="col-xs-12 col-md-6 col-lg-3"></div>
  <div class="col-xs-12 col-md-6 col-lg-3"></div>

</div>

</div>

<div class="row between-xs"> /* ceci signifie qu'à partir de la taille xs, donc mobile, toute les colonnes auront la même taille /*
```

### Grid Layout <a id ="grid"><a>

Documentation(https://mozilladevelopers.github.io/playground/css-grid/)

Cette technologie permet de créer une grille en fonction des éléments que l'on souhaite placé dans notre page. On définit le nombre de colonnes que l'on souhaite ainsi que le nombre de lignes. Par exemple si on souhaite 3 colonnes de 234px chacune et 4 lignes de 125px, avec un espacement de 2rem alors on écrit :

```css
.container {
 display: grid;
 grid-template-columns: 234px 234px 234px;
 grid-template-rows: 125px 125px 125px 125px;
 grid-gap: 2rem;
}
```
Cela nous permet d'obtenir une grille aux dimensions que l'on souhaite. Ainsi on peut placé nos éléments en fonction de celle-ci.Prénons l'exemple d'une image que l'on souhaite placé sur la premiére colonne à la deuxiéme ligne.


```css
.img1{
grid-column: 1 / 2;
grid-row: 2/ 4 ;
 width : 235px;
 height: 350px;
}
```


## SCSS <a id ="scss"><a>

*  ### Variables

Les variables permettent de stocker des informations afin de pouvoir les réutilisé plus tars dans la feuille de style. Cela permet d'optimisé notre style car en effet une couleur utilisé souvent dans notre style peut être modifier partout en un seul geste.
Les variables sont précédé d'un $.

-> _CSS_

```css

body {
  font-family: Helvetica, sans-serif;
  color: #333;
}

```

-> _SCSS_

```scss

$font-stack:    Helvetica, sans-serif;
$primary-color: #333;

body {
  font-family: $font-stack;
  color: $primary-color;
}
```

*  ### Nesting

Le Nesting permet de respecter la hiérarchie du HTML.

-> _CSS_

```css

nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

nav li {
  display: inline-block;
}

nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}

```
-> _SCSS_

```scss

nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li { display: inline-block; }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}

```

*  ### Les imports


-> _RESET_

```css

/* _reset.scss */

html,
body,
ul,
ol {
  margin:  0;
  padding: 0;
}

```

-> _CSS_

```css

/* base.scss */


@import 'reset';

body {
  font: 100% Helvetica, sans-serif;
  background-color: #efefef;
}

```

-> _SCSS_

```scss

html, body, ul, ol {
  margin: 0;
  padding: 0;
}

body {
  font: 100% Helvetica, sans-serif;
  background-color: #efefef;
}
```

*  ### Les Mixins <a id ="mixins"><a>

Une mixin permet de regrouper le style d'un élément et de l'appeler lorsqu'on en as besoin. Ainsi cela permet de ne pas réecrire le style pour un même élément comme pour des bouttons. Cela permet d'optimiser notre code.

-> _CSS_

```css
.button {
  padding: 14px 0;
  min-width: 100%;
  display: inline-block;
  border-radius: 4px;

  outline: none;
  cursor: pointer;
  background: #4D61D6;
  color: #fff;
  font-size: 14px;
  font-weight: 300;
  text-align: center;
  letter-spacing: .9px;
  transition: background .3s ease;
}
```
-> _SCSS_

```scss

@mixin generic-button {
  padding: 14px 0;
  min-width: 100%;
  display: inline-block;
  border-radius: 4px;

  outline: none;
  cursor: pointer;
  background: #4D61D6;
  color: #fff;
  font-size: 14px;
  font-weight: 300;
  text-align: center;
  letter-spacing: .9px;
  transition: background .3s ease;
}

button {
  @include generic-button;
}

```

### SVG :

- svg : l'attribut fill permet de remplir l'image de couleur cela évite d'avoir à l'importer de toute les couleurs.


### CSS Tips: <a id ="tips"><a>

__=> Box-sizing :__
</br>

* border-box

Permet de ne pas augmenter la taille d'une div. Si on as une div de 300px et qu'on veux un padding de 20px partout. On va utiliser box-sizing:borderbox pour ajouter les 20px de padding sans changer la taille de la div initiale. Quand vous ajoutez la propriété box-sizing: border-box; à un élément, le paddinget la bordure de cet élément n'augmentent plus sa largeur.

border-box indique au navigateur de prendre en compte la bordure et le remplissage dans la valeur définie pour la largeur et la hauteur. Autrement dit c'est le contenu de la boîte qui sera compressé pour absorber cette largeur supplémentaire.

* content-box

content-box est la valeur par défaut et correspond au comportement par défaut. Si on définit un élément avec une largeur de 100 pixels, la boîte de contenu de cet élément mesurera 100 pixels de large et la largeur de la bordure et/ou du remplissage sera alors ajoutée pour constituer la largeur finalement affichée.

__=> Direction:__

Permet de modifier la direction d'un texte ou d'un élément.

* ltr

La valeur par défaut qui correspond à une disposition de la gauche vers la droite pour le texte et les autres éléments.

* rtl

Le texte et les autres éléments vont de la droite vers la gauche.

__=> Position :__

* Static

static est la valeur par défaut de tous les éléments. Un élément avec position: static; n'est positionné d'aucune manière spéciale. Un élément static est dit non positionné et un élément avec une propriété position ayant une valeur autre que static est dit positionné.


```css
.static {
  position: static;
}
```

* Fixed

Un élément positionné en fixed est positionné par rapport a la fenêtre du navigateur, ce qui signifie qu'il reste toujours à la même place même si la page défile. De la même manière qu'avec un élément positionné en relative, nous pouvons utiliser les propriétés top, right, bottom et left.
Lorsqu'on met une div en fixed alors il faut utiliser un z-index sur toutes les autres div car fixed sort la div du flux.

```css
.fixed {
  position: fixed;
  bottom: 0;
  right: 0;
  width: 200px;
  background-color: white;
}
```


* Relative

relative se comporte de la même façon que static sauf si on ajoute quelques propriétés en plus.
Avec les propriétés top, right, bottom et left  un élément positionné en relative va le placer ailleurs que sa position normale. Le reste du contenu ne sera pas ajusté pour prendre la place dans l'espace laissé par l'élément.


```css
.relative1 {
  position: relative;
}
.relative2 {
  position: relative;
  top: -20px;
  left: 20px;
  background-color: white;
  width: 500px;
}
```
* Absolute

 absolute se comporte comme fixed sauf que son positionnement est relatif à l'élément parent positionné le plus proche au lieu d'être relatif à la fenêtre du navigateur. Si un élément positionné en absolute n'à aucun élément parent positionné, il utilise le corps du document et se déplace avec le document au défilement de la page.

```css
.relative {
  position: relative;
  width: 600px;
  height: 400px;
}
.absolute {
  position: absolute;
  top: 120px;
  right: 0;
  width: 300px;
  height: 200px;
}

```

## Font-face <a id ="font-face"><a>

La règle __@font-face__ permet de définir les polices d'écriture à utiliser pour afficher le texte de pages web. En permettant aux développeurs de fournir leurs propres polices, il n'est plus nécessaire de dépendre uniquement des polices qui sont installées sur les postes des utilisateurs.
Le but du __@font-face__ est de permettre au développeur d’utiliser une font non conventionnelle qui n’est hébergé dans aucun service webfont, en lui permettant de l’héberger en même temps que notre site. Ainsi on est sûr que  l’utilisateur pourra la visualiser. On crée ainsi ce que l’on appelle une police distante.

* __Etape 1 :__

Pour intégrer une typographie personnalisé il faut s’assurer que la typographie utilisé est de format:

.ttf : True Type
.otf : OpenType


* __Etape 2 :__

On télécharge la police qui nous intéresse. J’utilise le site : fontsquirrel.com  afin de trouver une typographie gratuite. Pour l’exemple j’ai télécharger la typographie Fira Sans.

* __Etape 3:__

Ensuite j’utilise le générateur Font Squirrel fin d’obtenir ma police en quatre formats différents : eot , svg, ttf, et woof. Cette étape sert à s’assurer que la police sera utilisable pour tout les navigateurs.


* __Etape 4 :__

Je transfert ma font dans mon dossier dev-absolute, dans le dossiers font afin qu’elle se trouve dans le même dossier que ma feuille de style.

* __Etape 5 :__  

Dans mon dossier font, j’obtient donc 1 fichier css (feuille de style) ainsi que 4 fichiers de typographie (eot , svg, ttf, et woof).  Ainsi je peux ouvrir ma feuille de style dans mon éditeur de texte, ce qui va me permettre d’obtenir le code __@font-face__ de chacune de mes quatre polices.


```css
@font-face{
  font-family: 'fira_sans_bold';
  src : url('firasans_bold-webfont.woff2') format('woff2'),
        url('firasans_bold-webfont.woff2') format('woff2');
  font-weight : normal;
  font-style: normal;
}

```


Je peux par conséquent copiez le code dans mon fichier css principal et supprimer ma feuille de style. Il va néanmoins falloir modifier ma source en fonction de la position de mon dossier afin d’indiquer le bon « chemin »  



      url('../fonts/firasansot-bold-webfont.svg#fira_sans_otbold')


J’utilise les  « .. /» afin de sortir du dossier css et d’entrer dans le dossier font

* __Etape 6:__

Grâce à cette démarche nous avons dorénavant la possibilité d’utilisé les attribut suivant dans notre css :

font-family  : désignant la police (‘Fira Sans’)
font-weight : désignant la graisse de la police (bold,normal,lighter)
font-style  : désignant le style de la police: normal, oblique,  italique

```css

.name{
  font-family: 'Fira Sans';
  font-weight: bold;
  font-style: oblique;
}

```


## Javascript


* ### Condition & Boucles <a id ="conditions&Boucles"><a>


=>  Les expressions conditionelles


  Les expressions conditionnelles s'appuient sur des opérateurs mathématiques __>, >=, <, <=__ qui testent si la première valeur est supérieure, supérieure ou égale, inférieure, inférieure ou égale à la seconde. Des opérateurs d'équivalence __==, !=, === et !==__ testent si deux valeurs sont égales/différentes qu'importe leur type ou égales/différentes et de même type.

```Javascript

 2  >   2; // → false
 2  >=  2; // → true
'2' ==  2; // → true
'2' !=  2; // → false
'2' === 2; // → false
'2' !== 2; // → true
 2  === 2; // → trues

```

L'expression conditionnelle __if__ effectue une opération si sa condition est vérifiée (égale àtrue). L'expression facultative else effectue une opération dans le cas inverse. Les opérations conditionnées par une de ces expressions sont encadrées par des accolades ouvrantes { et fermantes }.

```Javascript

if (song == 'A little help from my friend') {
  singer = 'Paul';
} else {
  singer = 'John';
}

```

=> Les opérateurs bouléens


Les opérateurs booléens __|| et &&__ représentent ou et et. L'opérateur __||__ retourne true si l'un de ces membres est évalué à true. L'opérateur __&&__ retourne true si tous ses membres sont évalués à true. En cas contraire, ces opérateurs retournent false.
L'opérateur __||__ évalue ses membres un à un jusqu'à trouver une valeur évaluée à true, il arrête d'évaluer ses membres dès qu'il en a trouvé une. L'opérateur __&&__ évalue ses membres un à un tant qu'il trouve une valeur évaluée à true, il arrête d'évaluer ses membres dès qu'il en a trouvé une false.

```Javascript

false || true;
→ true

false && true;
→ false

false || 5;
→ 5

false && 5;
→ false

```

=> L'expression de boucle while (Tant que)

Les boucles sont des expressions conditionnelles dont l'opération peut-être répétée à plusieurs reprises.
L'expression conditionnelle de boucle __while__ effectue une opération tant que sa condition est vérifiée (égale à __true__).


```Javascript

// compute 4! which is equal to 4*3*2*1

var fact = 4;
var total = 1;

while (fact > 0) {
  total = total * fact;
  fact = fact - 1;
}

// total === 24

```

Il est également possible d'utiliser le mot clé __do__ afin d'effectuer l'opération une première fois avant d'itérer.

```Javascript

do {
  total = total * fact;
  fact = fact - 1;
} while (fact > 0);

```


=> L'expression de boucle for

L'expression conditionnelle de boucle __for__ effectue une opération tant que sa condition est vérifiée (égale à true). L'initialisation est effectuée au premier pas de boucle, ensuite, tant que la condition n'est pas vérifiée;

La boucle __for__ comporte dans l'ordre une initialisation, une condition et une itération.

```Javascript

var notes = '';
for (var instruments = 0; instruments < 4; instruments++) {
    notes = notes + 'Ω';
}

notes;
→ 'ΩΩΩΩ' // après la boucle Ω à été augmenter de 4

```

* ### Tableaux & Dictionnaires <a id ="tableaux&Dictionnaires"><a>

=> Les tableaux

Les tableaux (Array), représentent une liste ordonnée de valeurs.

```Javascript

var alphabet = ['A','B','C', 'D'];

```

Un tableau commence sont index à 0. Donc dans l'exemple A correspond à 0. Il est également possible de modifier un tableau.


```Javascript

var alphabet = ['A', 'B'];
alphabet[3] = 'C';

```
Le nouveau tableau est → ['A', 'B', undefined, 'C']


=> Attributs et méthodes des tableaux


Les attributs et les méthodes sont proposés par le langage sur les tableaux afin de pouvoir les manipuler.

`length`indique le nombre d'élements d'un tableau <br>
`push(element1, …, elementN)` ajoute des éléments en dernière position <br>
`unshift(element1, …, elementN)` ajoute des éléments en première position <br>
`pop()` supprime le dernier élément <br>
`shift()` supprime le premier élément <br>
`sort()` trie les éléments (par défaut dans l'ordre croissant) <br>
`indexOf(element)` recherche la position d'un élément <br>
`splice(start, deleteCount)` supprime des éléments <br>
`reverse()` inverse l'ordre des éléments, le premier devenant le dernier, et ainsi de suite <br>
`join()` crée une chaîne de caractère en concaténant tous les éléments <br>
`concat(array1, …, arrayN)` concatène des tableaux à la suite <br>


=> Les dictionnaires

Les objets littéraux (Object) ou dictionnaire, représentent une suite de paires clé - valeur séparées par une virgule.

__Déclarer un dictionnaire__

```Javascript

var paul = {
  name: 'Paul',
  age: 72,
  guitar: true
};
```

__Ajout et modification dans un dictionnaire__

```Javascript

paul.guitar = false;
paul.bass = true;

delete paul.age;

paul;
→ {name: 'Paul', guitar: false, bass: true}

```

* ### Ajax <a id ="ajax"><a>

=> Xhr

En plus de permettre d'écouter les actions utilisateur et de modifier dynamiquement la page, JavaScript a une troisième fonctionnalité principale : la possibilité de requêter un serveur. C'est __l'AJAX (Asynchronous JavaScript and XML)__ qui permet cela. Il repose sur __l'objet XMLHttpRequest__ qui permet de se connecter à un serveur, de lui envoyer des données et d'en recevoir en retour. Elle utilise le protocole HTTP ; le navigateur émet une requête et attend une réponse du serveur. Cette requête est asynchrone, elle ne bloque pas le navigateur, qui peut continuer à interagir avec l'utilisateur, et sera notifié lors du retour du serveur.

Lorsque l'on utilise l'objet XMLHttpRequest on effectue une requête __xhr__.

__Requête ajax GET :__

```JavaScript

var xhr = new XMLHttpRequest();
xhr.open('GET', 'http://www.thebeatles.com/news', true);
xhr.setRequestHeader('Content-Type', 'application/json');

xhr.onload = function() {
  var status = xhr.status;
  var body = JSON.parse(xhr.responseText);

  /* use body as a classic dictionnary */
}
xhr.send();

```

__Requêtes ajax POST __

```JavaScript


var xhr = new XMLHttpRequest();
xhr.open("POST", "http://www.thebeatles.com/subscribe", true);
xhr.setRequestHeader("Content-Type", "application/json");

xhr.onload = function() {
  var body = JSON.parse(xhr.responseText);
  var status = xhr.status;
}
xhr.send(JSON.stringify({name:"contact@mail.com"}));

```

`open` configure la requête
`onload` permet de s'abonner à la réponse du serveur

Une fois la requête exécuter les attributs : `responseText` et `status` permettent de transformer la réponse obtenue en __JavaScript__

`send` permet d'effectuer l'appel


=> Fetch

Fetch n'est pas supporter par tout les navigateurs.

__Requête Fetch GET :__


```JavaScript

fetch('http://www.thebeatles.com/news')
.then(function(response) {
    return response.json();
})
.then(function(body) {
    /* use body as a classic dictionnary */
});

```

__Requête Fetch POST :__

```JavaScript
fetch('http://www.thebeatles.com/subscribe', {
    method: 'POST',
    json: JSON.stringify({name:"contact@mail.com"})
}).then(function(response) {
    return response.json();
})
.then(function(body) {
    /* use body as a classic dictionnary */
});
```

`response` représente le flux de données


### Liens utiles :

- [CssNext](http://cssnext.io/)
- [Grid Layout 1](https://mozilladevelopers.github.io/playground/css-grid/)
- [Grid Layout 2](https://css-tricks.com/snippets/css/complete-guide-grid/)
- [Squeleton](http://getskeleton.com/#grid)
- [FlexboxGrid 1](http://FlexboxGrid.com/)
- [FlexboxGrid 2](https://aerolab.co/blog/flexbox-grids/?utm_source=CSS-Weekly&utm_campaign=Issue-288&utm_medium=web)
- [Font-face 1](https://zellwk.com/blog/font-face/)
- [Font-face 2](https://developer.mozilla.org/fr/docs/Web/CSS/@font-face)
- [SVG optimizer](https://jakearchibald.github.io/svgomg/)
- [MOOC](https://github.com/yamsellem/hetic.js/raw/master/MOOC.zip)

### Sites de veilles

* [Awwwards](https://www.awwwards.com)
* [Codepen](https://codepen.io)
* [github](https://github.com/)
* [Codrops](https://tympanus.net/codrops)
* [Medium](https://medium.com)
