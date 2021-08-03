---
title: Fonctions et portée des fonctions
slug: Web/JavaScript/Reference/Functions
tags:
  - Function
  - JavaScript
  - Reference
translation_of: Web/JavaScript/Reference/Functions
original_slug: Web/JavaScript/Reference/Fonctions
---
<div>{{jsSidebar("Functions")}}</div>

<p>De manière générale, une fonction est un « sous-programme » qui peut être appelé par du code extérieur à la fonction (ou du code interne dans le cas d'une récursion). Comme le programme, une fonction est composée d'une suite d'instructions qui forment le <em>corps de la fonction</em>. Il est parfois possible de <em>passer</em> des valeurs à une fonction et une fonction peut éventuellement <em>retourner </em>(ou <em>renvoyer</em>) une valeur.</p>

<p>En JavaScript, les fonctions sont des objets de première classe. Cela signifie qu'elles peuvent être manipulées et échangées, qu'elles peuvent avoir des propriétés et des méthodes, comme tous les autres objets JavaScript. Les fonctions sont des objets {{jsxref("Objets_globaux/Function","Function")}}.</p>

<p>Pour plus d'informations et d'exemples, on pourra également consulter le <a href="/fr/docs/Web/JavaScript/Guide/Fonctions">chapitre du Guide JavaScript sur les fonctions.</a></p>

<h2 id="Description">Description</h2>

<p>Toute fonction JavaScript est en fait un objet <code>Function</code>. Voir la page {{jsxref("Objets_globaux/Function","Function")}} pour des informations sur les propriétés et les méthodes de ces objets.</p>

<p>Afin de renvoyer une valeur, la fonction doit comporter une instruction {{jsxref("Instructions/return","return")}} qui définit la valeur à renvoyer (sauf dans le cas d'un <a href="/fr/docs/Web/JavaScript/Reference/Objets_globaux/Object/constructor">constructeur</a> qui a été appelé avec le mot-clé {{jsxref("Opérateurs/L_opérateur_new")}}). Une fonction qui ne renvoie pas de valeur retourne {{jsxref("undefined")}}.</p>

<p>Les paramètres donnés lors de l'appel d'une fonction sont appelés les <em>arguments</em> de la fonction. Les arguments sont passés <em>par valeur</em> (<em>by value </em>en anglais). Si la fonction modifie la valeur d'un argument, ce changement ne se répercute pas en dehors de la fonction. Il existe cependant les <em>références</em> d'objets qui sont aussi des valeurs mais qui possèdent la particularité suivante : si la fonction modifie les propriété de l'objet de la référence, ce(s) changement(s) seront perceptibles en dehors de la fonction. Prenons l'exemple suivant :</p>

<pre class="brush: js"> /* Déclaration de la fonction 'maFonction' */
 function maFonction(monObjet)
 {
   monObjet.marque = "Toyota";
 }

 /*
  * Déclaration de la variable 'mavoiture';
  * création et initialisation d'un nouvel objet;
  * assigner une référence à 'mavoiture'
  */
 var mavoiture = {
   marque: "Honda",
   modele: "Accord",
   annee: 1998
 };

 /* Affiche 'Honda' */
 console.log(mavoiture.marque);

 /* Passer la référence de l'objet à la fonction */
 maFonction(mavoiture);

 /*
  * Affiche 'Toyota' pour valeur de la propriété 'marque'
  * de l'objet. C'est ce que la fonction a changé.
  */
 console.log(mavoiture.marque);
</pre>

<p>Le mot-clé <a href="/fr/docs/Web/JavaScript/Reference/Opérateurs/L_opérateur_this"><code>this</code></a> ne fait pas référence à la fonction en cours d'exécution. Il faut donc faire référence aux objets <code>Function</code> par leurs noms, et ce même au sein du corps de la fonction.</p>

<h2 id="Définir_des_fonctions">Définir des fonctions</h2>

<p>Il y a plusieurs façons de définir des fonctions</p>

<h3 id="Déclarer_une_fonction_linstruction_function">Déclarer une fonction (l'instruction <code>function</code>)</h3>

<p>Il existe une syntaxe spécifique pour la déclaration des fonctions (vous pouvez consulter la page de l'instruction {{jsxref("Instructions/function","function")}} pour plus de détails) :</p>

<pre class="syntaxbox">function <em>nom</em>([<em>param</em>[, <em>param</em>[, ... <em>param</em>]]]) {
   <em>instructions</em>
}
</pre>

<dl>
 <dt><code>nom</code></dt>
 <dd>Le nom de la fonction.</dd>
 <dt><code>param</code></dt>
 <dd>Le nom d'un argument à passer à la fonction (une fonction pouvant avoir jusqu'à 255 arguments).</dd>
 <dt><code>instructions</code></dt>
 <dd>Les instructions qui forment le corps de la fonction.</dd>
</dl>

<h3 id="Utiliser_une_expression_de_fonction_lexpression_function">Utiliser une expression de fonction (l'expression <code>function</code>)</h3>

<p>L'expression d'une fonction se fait d'une façon similaire à la déclaration (veuillez consulter la page de l'expression {{jsxref("Opérateurs/L_opérateur_function","function")}} pour plus d'informations) :</p>

<pre class="syntaxbox">function [<em>nom</em>]([<em>param</em>] [, <em>param</em>] [..., <em>param</em>]) {
   <em>instructions</em>
}
</pre>

<dl>
 <dt><code>nom</code></dt>
 <dd>Le nom de la fonction. Il est facultatif, auquel cas la fonction devient une fonction anonyme.</dd>
 <dt><code>param</code></dt>
 <dd>Le nom d'un argument à passer à la fonction.</dd>
 <dt><code>instructions</code></dt>
 <dd>Les instructions qui forment le corps de la fonction.</dd>
</dl>

<p>Voici un exemple d'expression de fonction <strong>anonyme</strong> (il n'y a pas de nom utilisé) :</p>

<pre class="brush: js">var maFonction = function() {
  /* instructions */
}</pre>

<p>Il est également possible de fournir un nom lors de la définition afin de créer une expression de fonction <strong>nommée</strong> :</p>

<pre class="brush: js">var maFonction = function fonctionNommée(){
  /* instructions */
}
</pre>

<p>L'un des bénéfices d'utiliser une expression de fonction nommée est que son nom sera utilisé dans la pile d'appel lors qu'on aura une erreur. Avec le nom de la fonction, il sera plus facile de repérer l'origine de l'erreur.</p>

<p>Comme on peut le voir, ces deux derniers exemples ne commencent pas avec le mot-clé <code>function</code>. Les instructions qui déclarent des fonctions mais qui ne commencent pas avec <code>function</code> sont des expressions de fonction.</p>

<p>Lorsque les fonctions sont utilisées une unique fois, on peut utiliser une <a href="/fr/docs/Glossaire/IIFE">« expression de fonction immédiatement invoquée » (ou plus généralement appelée <em>IIFE</em> pour <em>Immediately Invokable Function Expression</em> en anglais)</a>.</p>

<pre class="brush: js">(function() {
    /* instruction */
})();</pre>

<p>Les <em>IIFE</em> sont des expressions de fonction appelées dès que la fonction est déclarée.</p>

<h3 id="Utiliser_une_déclaration_de_fonction_génératrice_linstruction_function*">Utiliser une déclaration de fonction génératrice (l'instruction <code>function*</code>)</h3>

<p>Il existe une syntaxe spéciale pour déclarer des générateurs (voir la page sur l'instruction {{jsxref('Instructions/function*', 'function*')}} pour plus de détails) :</p>

<pre class="syntaxbox">function* <em>nom</em>([<em>param</em>[, <em>param</em>[, ... <em>param</em>]]]) {
   <em>instructions</em>
}</pre>

<dl>
 <dt><code>nom</code></dt>
 <dd>Le nom de la fonction.</dd>
 <dt><code>param</code></dt>
 <dd>Le nom d'un argument à passer à la fonction.</dd>
 <dt><code>instructions</code></dt>
 <dd>Les instructions qui forment le corps de la fonction.</dd>
</dl>

<h3 id="Utiliser_une_expression_de_générateur_lexpression_function*">Utiliser une expression de générateur (l'expression <code>function*</code>)</h3>

<p>Une expression de générateur est similaire à une déclaration de fonction génératrice et possède presque la même syntaxe (pour plus de détails, consulter la page sur l'expression {{jsxref('Opérateurs/function*', 'function*')}}) :</p>

<pre class="syntaxbox">function* [<em>nom</em>]([<em>param</em>[, <em>param</em>[, ... <em>param</em>]]]) {
   <em>instructions</em>
}</pre>

<dl>
 <dt><code>nom</code></dt>
 <dd>Le nom de la fonction. Ce paramètre peut être omis, auquel cas la fonction sera une fonction anonyme.</dd>
 <dt><code>param</code></dt>
 <dd>Le nom d'un argument à passer à la fonction.</dd>
 <dt><code>instructions</code></dt>
 <dd>Les instructions qui composent le corps de la fonction.</dd>
</dl>

<h3 id="Utiliser_une_expression_de_fonction_fléchée_>">Utiliser une expression de fonction fléchée (=&gt;)</h3>

<p>Une expression de fonction fléchée possède une syntaxe plus courte et est liée, de façon lexicale, à sa valeur (voir la page sur les <a href="/fr/docs/Web/JavaScript/Reference/Fonctions/Fonctions_fl%C3%A9ch%C3%A9es">fonctions fléchées</a> pour plus de détails) :</p>

<pre class="syntaxbox">([param[, param]]) =&gt; {
   instructions
}

param =&gt; expression
</pre>

<dl>
 <dt><code>param</code></dt>
 <dd>Le nom d'un argument. S'il n'y a pas d'arguments, cela doit être indiqué par <code>()</code>.  S'il y a un seul argument, les parenthèses ne sont pas obligatoires (par exemple :  <code>toto =&gt; 1</code>).</dd>
 <dt><code>instructions </code>ou<code> expression</code></dt>
 <dd>S'il y a plusieurs instructions, elles doivent être encadrées par des accolades. Une expression unique ne doit pas obligatoirement être entourée d'accolades. L'expression est également la valeur de retour implicite de la fonction.</dd>
</dl>

<h3 id="Le_constructeur_Function">Le constructeur <code>Function</code></h3>

<div class="note">
<p><strong>Note :</strong> L'utilisation du constructeur <code>Function</code> afin de créer des fonction n'est pas recommandée. En effet, il utilise une chaîne pour former le corps de la fonction et cela peut empêcher certaines optimisations du moteur JavaScript ainsi que provoquer d'autres problèmes.</p>
</div>

<p>Comme tous les autres objets, les objets {{jsxref("Function")}} peuvent être créés grâce à l'opérateur <code>new</code> :</p>

<pre class="syntaxbox">new Function (<em>arg1</em>, <em>arg2</em>, ... <em>argN</em>, <em>corpsDeLaFonction</em>)
</pre>

<dl>
 <dt><code>arg1, arg2, ... argN</code></dt>
 <dd>Plusieurs (zéro ou plus) noms qui seront utilisés par la fonction comme noms d'arguments formels. Chaque nom doit être une chaîne de caractères valide au sens d'un identifiant JavaScript ou alors être une liste de telles chaînes séparées par des virgules. On aura les exemples suivants : "<code>x</code>", "<code>laValeur</code>", ou "<code>a,b</code>".</dd>
 <dt><code>corpsDeLaFonction</code></dt>
 <dd>Une chaîne de caractères contenant les instructions JavaScript définissant la fonction.</dd>
</dl>

<p>L'invocation du constructeur <code>Function</code> en tant que fonction (sans utiliser l'opérateur <code>new</code>) a le même effet que son invocation en tant que constructeur.</p>

<h3 id="Le_constructeur_GeneratorFunction">Le constructeur <code>GeneratorFunction</code></h3>

<div class="note">
<p><strong>Note :</strong> <code>GeneratorFunction</code> n'est pas un objet global mais pourrait être obtenu à partir de l'instance de la fonction génératrice (voir la page {{jsxref("GeneratorFunction")}} pour plus de détails).</p>
</div>

<div class="note">
<p><strong>Note :</strong> Le constructeur <code>GeneratorFunction</code> ne doit pas être utilisé pour créer des fonctions. En effet, il utilise une chaîne pour former le corps de la fonction et cela peut empêcher certaines optimisations du moteur JavaScript ainsi que provoquer d'autres problèmes.</p>
</div>

<p>Comme pour tous les autres objets, les objets {{jsxref("GeneratorFunction")}} peuvent être créés grâce à l'opérateur <code>new</code> :</p>

<pre class="syntaxbox">new GeneratorFunction (<em>arg1</em>, <em>arg2</em>, ... <em>argN</em>, <em>corpsFonction</em>)</pre>

<dl>
 <dt><code>arg1, arg2, ... arg<em>N</em></code></dt>
 <dd>Plusieurs (zéro ou plus) noms qui seront utilisés par la fonction comme noms d'arguments formels. Chaque nom doit être une chaîne de caractères valide au sens d'un identifiant JavaScript ou alors être une liste de telles chaînes séparées par des virgules. On aura les exemples suivants : "<code>x</code>", "<code>theValue</code>", ou "<code>a,b</code>".</dd>
 <dt><code>corpsFonction</code></dt>
 <dd>Une chaîne de caractères contenant les instructions JavaScript définissant la fonction.</dd>
</dl>

<h2 id="Les_paramètres_dune_fonction">Les paramètres d'une fonction</h2>

<h3 id="Les_paramètres_par_défaut">Les paramètres par défaut</h3>

<p>Les paramètres par défaut permettent aux paramètres déclarés d'une fonction de pouvoir être initialisés avec des valeurs par défaut s'ils ne sont pas fournis à la fonction ou s'ils valent <code>undefined</code>. Pour plus de détails, voir la page de la référence sur <a href="/fr/docs/Web/JavaScript/Reference/Fonctions/Valeurs_par_défaut_des_arguments">les paramètres par défaut</a>.</p>

<h3 id="Les_paramètres_du_reste">Les paramètres du reste</h3>

<p>Cette syntaxe permet de représenter un nombre indéfini d'arguments sous forme d'un tableau. Pour plus de détails, voir la page sur <a href="/fr/docs/Web/JavaScript/Reference/Fonctions/param%C3%A8tres_du_reste">les paramètres du reste</a>.</p>

<h2 id="Lobjet_arguments">L'objet <code>arguments</code></h2>

<p>Il est possible de faire référence aux arguments d'une fonction au sein de cette fonction en utilisant l'objet <code>arguments</code>. Consulter la page <a href="/fr/docs/Web/JavaScript/Reference/Fonctions/arguments">arguments</a> pour plus d'informations.</p>

<ul>
 <li><code><a href="/fr/docs/Web/JavaScript/Reference/Fonctions/arguments">arguments</a></code> : Un objet semblable à un tableau qui contient les arguments passés à la fonction qui est exécutée.</li>
 <li><code><a href="/fr/docs/Web/JavaScript/Reference/Fonctions/arguments/callee">arguments.callee</a></code> {{Deprecated_inline}} : La fonction en cours d'exécution.</li>
 <li><code><a href="/fr/docs/Web/JavaScript/Reference/Fonctions/arguments/caller">arguments.caller</a></code> {{Obsolete_inline}} : La fonction qui a appelé la fonction courante.</li>
 <li><code><a href="/fr/docs/Web/JavaScript/Reference/Fonctions/arguments/length">arguments.length</a></code> : Le nombre d'arguments passés à la fonction.</li>
</ul>

<h2 id="Récursion">Récursion</h2>

<p>Une fonction peut faire référence à elle-même et s'appeler elle-même. Il y a trois façons pour qu'une fonction fasse appel à elle-même :</p>

<ol>
 <li>le nom de la fonction</li>
 <li><code><a href="/fr/docs/Web/JavaScript/Reference/Fonctions/arguments/callee">arguments.callee</a></code></li>
 <li>une variable interne faisant référence à la fonction</li>
</ol>

<p>Avec l'exemple suivant :</p>

<pre class="brush: js">var truc = function toto() {
   // instructions
};
</pre>

<p>Ce qui suit sera équivalent au sein de la fonction :</p>

<ol>
 <li><code>toto()</code></li>
 <li><code>arguments.callee()</code></li>
 <li><code>truc()</code></li>
</ol>

<p>Une fonction qui s'appelle elle-même est appelée une fonction récursive. D'une certaine manière, une récursion est semblable à une boucle. Une récursion et une boucle exécutent le même code plusieurs fois et s'appuient sur une condition (afin d'éviter une boucle infinie, ou plutôt une récursion infinie ici). Ainsi la boucle suivante :</p>

<pre class="brush: js">var x = 0;
// "x &lt; 10" est la condition de la boucle
while (x &lt; 10) {
   // faire des choses
   x++;
}
</pre>

<p>peut être convertie en une fonction récursive et un appel à cette fonction :</p>

<pre class="brush: js">function boucle(x) {
   // "x &gt;= 10" est la condition de sortie
   // (et équivaut à "!(x &lt; 10)")
   if (x &gt;= 10)
      return;
   // faire des choses
   boucle(x + 1); // l'appel récursif
}
boucle(0);
</pre>

<p>Cependant, certains algorithmes ne peuvent pas être traduits sous forme de boucles itératives. Ainsi, obtenir tous les nœuds d'un arbre (par exemple le DOM), est beaucoup plus facile à faire de manière récursive.</p>

<pre class="brush: js">function parcoursArbre(noeud) {
   if (noeud == null) //
      return;
   // faire quelque chose avec le noeud
   for (var i = 0; i &lt; noeud.childNodes.length; i++) {
      parcoursArbre(noeud.childNodes[i]);
   }
}
</pre>

<p>Par rapport à la fonction <code>boucle</code>, chaque appel récursif enchaîne ici plusieurs appels récursifs successifs.</p>

<p>Il est théoriquement possible de convertir tout algorithme récursif en un algorithme non-récursif. Cependant, la logique du problème est souvent beaucoup plus complexe et l'on doit faire recours à une pile pour le résoudre. Mais la récursion n'est en fait rien d'autre que l'utilisation d'une pile : la pile de la fonction.</p>

<p>La comportement de la récursion en tant que pile peut être observée avec cet exemple :</p>

<pre class="brush: js">function truc(i) {
   if (i &lt; 0)
      return;
   console.log('début :' + i);
   toto(i - 1);
   console.log('fin :' + i);
}
truc(3);
</pre>

<p>Elle produira le résultat suivant :</p>

<pre class="brush: js">début :3
début :2
début :1
début :0
fin :0
fin :1
fin :2
fin :3
</pre>

<h2 id="Fonctions_imbriquées_et_fermetures">Fonctions imbriquées et fermetures</h2>

<p>Il est possible d'imbriquer une fonction au sein d'une fonction. La fonction imbriquée (interne) est privée par rapport à la fonction (externe) qui la contient. Cela forme ce qu'on appelle une fermeture (<em>closure</em> en anglais).</p>

<p>Une fermeture est une expression (généralement une fonction) possédant des variables libres ainsi qu'un environnement qui lie ces variable (autrement dit qui « ferme » l'expression).</p>

<p>Étant donné qu'une fonction imbriquée est une fermeture, cela signifie que la fonction imbriquée peut « hériter » des arguments et des variables de la fonction qui la contient. En d'autres termes, la fonction interne contient la portée de la fonction externe.</p>

<p>Pour résumer :</p>

<ul>
 <li>on ne peut accéder à la fonction interne seulement avec des instructions contenues dans la fonction externe,</li>
</ul>

<ul>
 <li>la fonction interne est une fermeture : la fonction interne peut utiliser des arguments et des variables de la fonction externe alors que la fonction externe ne peut pas utiliser de variables et d'arguments de la fonction interne.</li>
</ul>

<p>L'exemple suivant, montre le cas de fonctions imbriquées :</p>

<pre class="brush: js">function ajouteCarres(a,b) {
   function carre(x) {
      return x * x;
   }
   return carre(a) + carre(b);
}
var a = ajouteCarres(2,3); // renvoie 13
var b = ajouteCarres(3,4); // renvoie 25
var c = ajouteCarres(4,5); // renvoie 41
</pre>

<p>Étant donné que la fonction interne est une fermeture, il est possible d'appeler la fonction externe et de définir des arguments pour la fonction externe mais aussi pour la fonction interne :</p>

<pre class="brush: js">function externe(x) {
   function interne(y) {
      return x + y;
   }
   return interne;
}
var fn_interne = externe(3);
var resultat = fn_interne(5); // renvoie 8

var resultat1 = externe(3)(5); // renvoie 8
</pre>

<h3 id="Conservation_des_variables">Conservation des variables</h3>

<p>On voit alors que <code>x</code> est conservé lorsqu'<code>interne</code> est renvoyé. Une fermeture doit conserver les arguments et les variables au sein de toutes les portées auxquelles elle fait référence. Étant donné qu'éventuellement, chaque appel fournira des arguments différents, une nouvelle fermeture est créée pour chaque appel externe. La mémoire peut donc être libérée seulement lorsque <code>inside</code> n'est plus accessible.</p>

<p>Cela n'est pas différent du stockage de références avec d'autres objets, mais ça reste plus délicat à observer puisqu'on ne peut inspecter ou définir soi-même les références en question.</p>

<h3 id="Imbrication_multiple_de_fonctions">Imbrication multiple de fonctions</h3>

<p>On peut imbriquer plusieurs fonctions : une fonction (A) contien une fonction (B) qui contient une fonction (C). Ici les fonctions B et C forment des fermetures et aisni B peut accéder à A et C peut accéder à B. On peut donc en déduire, puisque C accède à B qui accède à A que C peut accéder à A. On voit donc que les fermetures peuvent contenir différentes portées. Elles peuvent, récursivement, contenir la portée des fonctions qui la contiennent. Ce mécanisme est appelé « chaînage de portée »  (<em>scope chaining</em> en anglais). (Cette dénomination sera expliquée par la suite.)</p>

<p>On peut l'observer avec l'exemple suivant :</p>

<pre class="brush: js">function A(x) {
   function B(y) {
      function C(z) {
         console.log(x + y + z);
      }
      C(3);
   }
   B(2);
}
A(1); // crée un message d'alerte avec 6 (= 1 + 2 + 3)
</pre>

<p>Dans cet exemple, C accède à la variable y de B et à la variable x de A. Cela est possible parce que :</p>

<ol>
 <li><code>B</code> est une fermeture qui contient <code>A</code>, autrement dit <code>B</code> peut accéder aux arguments et aux variables de <code>A</code></li>
 <li><code>C</code> est une fermeture qui contient <code>B</code></li>
 <li>Étant donné que la fermeture de <code>B</code> contient <code>A</code> et que celle de <code>C</code> contient <code>B</code>, <code>C</code> peut accéder à la fois aux arguments et variables de <code>B</code> <em>et</em> <code>A</code>. Autrement dit, <code>C</code> <em>enchaîne les portées de </em> <code>B</code> et <code>A</code> dans cet ordre.</li>
</ol>

<p>La réciproque n'est pas vraie. <code>A</code> ne peut avoir accès à <code>C</code>, parce que <code>A</code> ne peut accéder ni aux variables ni aux arguments de <code>B</code>, or <code>C</code> est une variable de <code>B. C</code> est donc privé et seulement pour <code>B</code>.</p>

<h3 id="Conflits_de_noms">Conflits de noms</h3>

<p>Lorsque deux arguments ou variables appartenant aux portées d'une fermeture ont le même nom, il y a un <em>conflit de noms</em>. La portée la plus interne l'emportera par rapport à la portée la plus externe. C'est ce qu'on appelle la chaîne de portée (<em>scope chain</em> en anglais). Le premier maillon de cette chaîne est la portée la plus interne tandis que le dernier maillon est représenté par la portée la plus externe. Regardons l'exemple suivant :</p>

<pre class="brush: js">function externe() {
   var x = 10;
   function interne(x) {
      return x;
   }
   return interne;
}
resultat = externe()(20); // renvoie 20 et non pas 10
</pre>

<p>Le conflit de nom apparaît avec l'instruction <code>return x</code> et vient de la dénomination commune de l'argument <code>x </code>de la fonction<code> interne</code> et la variable <code>x </code>de la fonction <code>externe</code>. La chaîne de portée est, pour cet exemple : {<code>interne</code>, <code>externe</code>, objet globalt}. On voit alors que le  <code>x</code> de la fonction interne l'emporte sur le <code>x </code>de la fonction externe. 20 (<code>x</code> de la fonction <code>interne</code>) est donc renvoyé plutôt que 10 (<code>x</code> de la fonction <code>externe</code>).</p>

<h2 id="Définition_des_méthodes">Définition des méthodes</h2>

<h3 id="Les_accesseurs_et_mutateurs_getter_et_setter">Les accesseurs et mutateurs (<em>getter</em> et <em>setter</em>)</h3>

<p>Il est possible de définir des méthodes qui sont accesseurs ou des mutateurs sur n'importe quel objet qui peut avoir de nouvelles propriétés. La syntaxe utilisée pour définir les <em>getters</em> et <em>setters</em> est celle utilisée avec les littéraux objets.</p>

<dl>
 <dt><a href="/fr/docs/Web/JavaScript/Reference/Fonctions/get">get</a></dt>
 <dd>
 <p>Permet de lier une propriété d'un objet à une fonction qui sera appelée lorsqu'on accèdera à la propriété.</p>
 </dd>
 <dt><a href="/fr/docs/Web/JavaScript/Reference/Fonctions/set">set</a></dt>
 <dd>Permet de lier une propriété d'un objet à une fonction qui sera appelée lorsqu'on tentera de modifier cette propriété.</dd>
</dl>

<h3 id="Syntaxe_des_définitions_de_méthode_ECMAScript_2015">Syntaxe des définitions de méthode ECMAScript <strong>2015</strong></h3>

<p>Avec ECMAScript 2015, il est possible de définir des méthodes de façon plus concise (à la façon de ce qui est déjà possible pour les getters et setters). Voir la page sur <a href="/fr/docs/Web/JavaScript/Reference/Fonctions/Définition_de_méthode">les définitions de méthodes</a> pour plus d'informations.</p>

<pre class="brush: js">var obj = {
  toto() {},
  truc() {}
};</pre>

<h2 id="Constructeur_déclaration_expression">Constructeur, déclaration, expression ?</h2>

<p>Comparons les exemples suivants :</p>

<ol>
 <li>une fonction définie grâce au constructeur <code>Function</code> assignée à la variable <code>multiplier</code>

  <pre class="brush: js">var multiplier = new Function("x", "y", "return x * y;");
</pre>
 </li>
 <li>une déclaration de fonction d'une fonction appelée <code>multiplier</code>
  <pre class="brush: js">function multiplier(x, y) {
   return x * y;
}
</pre>
 </li>
 <li>une expression de fonction d'une fonction anonyme assignée à la variable <code>multiplier</code>
  <pre class="brush: js">var multiplier = function(x, y) {
   return x * y;
};
</pre>
 </li>
 <li>une expression de fonction d'une fonction nommée <code>fonction_nom</code> assignée à la variable <code>multiplier</code>
  <pre class="brush: js">var multiplier = function function_nom(x, y) {
   return x * y;
};
</pre>
 </li>
</ol>

<p>Tous ces exemples effectuent à peu près la même chose, mais différent sur quelques points :</p>

<ul>
 <li>Il y a une distinction entre le nom de la fonction et la variable à laquelle elle est affectée :
  <ul>
   <li>le nom de la fonction ne peut être changé alors que la variable à laquelle la fonction a été assignée peut être réassignée.</li>
   <li>le nom de la fonction ne peut-être utilisé qu'à l'intérieur du corps de la fonction. Toute tentative d'utilisation en dehors du corps de la fonction entraînera une erreur (ou <code>undefined</code> si le nom de la fonction a été déclaré auparavant avec une instruction <code>var</code>). Ainsi :
    <pre class="brush: js">var y = function x() {};
console.log(x); // renvoie une erreur
</pre>

    <p>Le nom de la fonction apparaît également lorsque la fonction est sérialisée avec la <a href="/fr/docs/JavaScript/Reference/R%C3%A9f%C3%A9rence_JavaScript/Objets_globaux/Function/toString">méthode toString de l'objet <code>Function</code></a>.</p>

    <p>La variable à laquelle est assignée la fonction est seulement limitée par rapport à la portée. La portée au sein de laquelle la fonction est déclarée est donc garantie d'être dans la portée de la variable.</p>
   </li>
   <li>Comme le montre le quatrième exemple, le nom de la fonction peut être différent du nom de la variable à laquelle a été assignée la fonction. Les deux noms n'ont aucune relation entre eux.</li>
  </ul>
 </li>
 <li>Une déclaration de fonction peut aussi créer une variable avec le même nom que la fonction. Ainsi, contrairement une expression de fonction, une déclaration de fonction permet d'accéder à la fonction grâce à son nom au sein de la portée dans laquelle elle a été définie :
  <pre class="brush: js">function x() {}
console.log(x); // affichera la fonction x sérialisée en une chaîne de caractères
</pre>

  <p>L'exemple qui suit montre que les noms de fonctions ne sont par liées aux variables auxquelles sont assignées les fonctions. Si une variable de fonction est assignée à une autre valeur, elle aura toujours le même nom de fonction :</p>

  <pre class="brush: js">function toto() {}
console.log(toto); // message affichant la chaine de caractères "toto"
var truc = toto;
console.log(truc); // message affichant la chaine de caractères "toto"
</pre>
 </li>
 <li>Une fonction définie grâce à « <code>new Function »</code> n'aura pas de nom de fonction. Cependant, le moteur JavaScript <a href="/fr/docs/SpiderMonkey">SpiderMonkey</a>, la forme sérialisée de la fonction apparaît comme si la fonction avait le nom « anonymous ». Le code <code>console.log(new Function())</code> produira :
  <pre class="brush: js">function anonymous() {
}
</pre>

  <p>La fonction n'ayant pas de nom effectif, <code>anonymous</code> n'est pas une variable à laquelle on pourra accéder au sein de la fonction. Par exemple, le code qui suit produira une erreur :</p>

  <pre class="brush: js">var toto = new Function("console.log(anonymous);");
toto();
</pre>
 </li>
 <li>À la différence des fonctions définies par les expressions de fonction ou par le constructeur <code>Function</code>, une fonction définie par une déclaration de fonction pourra être utilisée avant la déclaration. Ainsi :
  <pre class="brush: js">toto(); // affichera TOTO !
function toto() {
   console.log('TOTO !');
}
</pre>
 </li>
 <li>Une fonction définie par une expression de fonction hérite de la portée courante. La fonction forme donc une fermeture. En revanche, les fonctions définies par le constructeur <code>Function</code> n'héritent que de la portée globale (portée héritée par toutes les fonctions).</li>
 <li>Les fonctions définies par les expressions et les déclarations de fonctions ne sont analysées (parsées) qu'une seule fois. Celles définies grâce au constructeur <code>Function</code> ne le sont pas. Cela signifie que la chaîne de caractère représentant le corps de la fonction doit être analysée à chaque fois qu'elle est évaluée. Bien qu'une expression de fonction crée obligatoirement une fermeture, le corps de la fonction n'est pas parsé à nouveau. Les expressions de fonctions sont donc plus rapides que « <code>new Function(...)</code> ». Il faut donc éviter le constructeur <code>Function</code> autant que possible.<br>
  Il faut cependant noter que les expressions et les déclarations imbriquées au sein d'une chaîne de caractère pour un constructeur <code>Function</code> ne sont analysées qu'une seule fois. On aura l'exemple suivant :
  <pre class="brush: js">var toto = (new Function("var truc = \'TOTO !\';\nreturn(function() {\n\tconsole.log(truc);\n});"))();
toto(); //La partie « function() {\n\tconsole.log(truc);\n} » de la chaîne de caractères n'est pas analysée à nouveau.</pre>
 </li>
</ul>

<p>Une déclaration de fonction peut très facilement (et souvent involontairement) être transformée en une expression de fonction. Une déclaration de fonction cesse d'en être une lorsque :</p>

<ul>
 <li>elle fait partie d'une expression</li>
 <li>ou elle n'est plus un « élément source » de la fonction ou du script. Un « élément source » est une instruction non-imbriquée du script ou d'un corps de fonction.
  <pre class="brush: js">var x = 0;                 // élément source
if (x === 0) {              // élément source
   x = 10;                 // pas un élément source
   function titi() {}      // pas un élément source
}
function toto() {          // élément source
   var y = 20;             // élément source
   function truc() {}      // élément source
   while (y === 10) {       // élément source
      function machin() {} // pas un élément source
      y++;                 // pas un élément source
   }
}
</pre>
 </li>
</ul>

<h3 id="Exemples">Exemples :</h3>

<ul>
 <li>
  <pre class="brush: js">// déclaration de fonction
function toto() {}

// expression de fonction
(function truc() {})

// expression de fonction
var x = function bonjour() {}</pre>
 </li>
 <li>
  <pre class="brush: js">if (x) {
   // expression de fonction
   function monde() {}
}
</pre>
 </li>
 <li>
  <pre class="brush: js">// déclaration de fonction
function a() {
   // déclaration de fonction
   function b() {}
   if (0) {
      // expression de fonction
      function c() {}
   }
}
</pre>
 </li>
</ul>

<h2 id="Définir_une_fonction_de_façon_conditionnelle">Définir une fonction de façon conditionnelle</h2>

<p>Il est possible de définir des fonctions de manière conditionnelle en utilisant soit : //function statements// (une extension autorisée par le standard <a href="https://www.ecma-international.org/publications/standards/Ecma-262.htm">ECMA-262 Edition 3</a>) soit le constructeur <code>Function</code>. Il faut noter que de telles instructions ne sont plus autorisées dans le standard <a class="link-https" href="https://bugzilla.mozilla.org/show_bug.cgi?id=609832">ES5 strict</a>. Il faut également savoir que cela ne fonctionne pas de manière homogène sur les différents navigateurs. Il est donc déconseillé d'utiliser cette fonctionnalité.</p>

<p>Dans le script qui suit, la fonction <code>zero</code> n'est jamais définie et ne peut donc être appelée car le test « <code>if (0)</code> » est toujours faux :</p>

<pre class="brush: js">if (0) {
   function zero() {
      console.log("C'est zero.");
   }
}
</pre>

<p>Si le script est changé et que la condition devient « <code>if (1)</code> », la fonction <code>zero</code> sera alors définie.</p>

<p>Bien que cette fonction ressemble à une déclaration de fonction, il s'agit en fait d'une expression (ou instruction) de fonction, car celle-ci est imbriquée au sein d'une autre instruction. (Consulter le paragraphe précédent pour une explication à ce sujet).</p>

<div class="note">
<p><strong>Note :</strong> À la différence de <a href="/fr/docs/SpiderMonkey">SpiderMonkey</a>, certains moteurs JavaScript traîtent incorrectement les expressions de fonction avec un nom comme des définitions de fonction. Cela conduirait à la définition de la fonction <code>zero</code> et ce même avec la condition <code>if</code> valant faux. Une façon plus sûre de définir des fonctions de manière conditionnelle est de définir la fonction et de l'assigner à une variable :</p>

<pre class="brush: js">if (0) {
   var zero = function() {
      console.log("C'est zero");
   }
}
</pre>
</div>

<h2 id="Les_fonctions_en_tant_que_gestionnaires_dévénements">Les fonctions en tant que gestionnaires d'événements</h2>

<p>En JavaScript, les gestionnaires d'événements <a href="/fr/docs/DOM">DOM</a> (<em>event handlers</em> en anglais) sont des fonctions (différentes des objets contenant une méthode <code>handleEvent</code> dans d'autres langages de liaison avec le DOM -<em>binding languages</em> en anglais). Les fontions ont l'objet <a href="/fr/docs/DOM/event">event</a> comme seul et unique paramètre. Comme tous les autres paramètres, si l'objet événement, n'a pas besoin d'être utilisé, il peut être absent de la liste des paramètres formels.</p>

<p>Les objets d'un document HTML susceptibles de recevoir des événements peuvent être par exemple : <code>window</code> (objets<code> Window</code>, y compris les objets frames), <code>document</code> (les objets <code>HTMLDocument</code>), et les éléments (les objets <code>Element</code>). Au sein du <a href="https://www.w3.org/TR/DOM-Level-2-HTML/">DOM HTML</a>, les objets recevant des événements possède des propriétés gestionnaires d'événements. Ces propriétés sont les noms des événements en minuscules préfixés par « on » (par exemple <code>onfocus</code>). Une autre façon, plus fiable, d'ajouter des auditeurs d'événements, est offert par les <a href="https://www.w3.org/TR/DOM-Level-2-Events/">événements DOM de niveau 2</a>.</p>

<p>Note : Les événements font partie de la logique DOM et non de celle de JavaScript. (JavaScript n'est qu'un langage permettant de manipuler le DOM.)</p>

<p>L'exemple suivant assigne une fonction au gestionnaire de l'événement « focus ».</p>

<pre class="brush: js">window.onfocus = function() {
   document.body.style.backgroundColor = 'white';
};
</pre>

<p>Si une fonction est assignée à une variable, il est possible d'assigner la variable à un gestionnaire d'événement. Le fragment de code qui suit assigne une fonction à la variable <code>setBGColor</code>.</p>

<pre class="brush: js">var setBGColor = new Function("document.body.style.backgroundColor = 'white';");
</pre>

<p>Il est alors possible d'utiliser cette variable pour assigner une fonction à un gestionnaire d'événement. Cela peut se faire de plusieurs manières, en voici deux décrites ici :</p>

<ol>
 <li>écrire dans les propriétés de l'évément DOM HTML
  <pre class="brush: js">document.form1.colorButton.onclick = setBGColor;
</pre>
 </li>
 <li>l'attribut de l'événement HTML
  <pre class="brush: html">&lt;input type="button"
   value="Changer la couleur de fond"
   onclick="setBGColor();"/&gt;
</pre>

  <p>Un gestionnaire d'événement défini de cette manière sera une fonction, nommée selon l'attribut, encadré du code spécifique nécessaire. C'est pourquoi les parenthèses sont ici nécessaires (<code>setBGColor()</code> et non pas <code>setBGColor</code>). Cela est équivalent à :</p>

  <pre class="brush: js">document.form1.colorButton.onclick = function onclick(event) {
   setBGColor();
};
</pre>

  <p>Il faut noter la façon dont l'objet événement est passé à la fonction en tant que paramètre <code>event</code>. Cela permet au code d'utiliser l'objet <code>Event</code> :</p>

  <pre class="brush: html">&lt;input ...
    onclick="console.log(event.target.tagName);"/&gt;
</pre>
 </li>
</ol>

<p>Tout comme les autres propriétés faisant référence à une fonction, le gestionnaire d'événement peut agir come une méthode et <code>this</code> ferait alors référence à l'élément contenant le gestionnaire d'événement. Dans l'exemple suivant, la fonction à laquelle <code>onfocus</code> fait référence est appelée avec <code>this</code> qui a la valeur <code>window</code>.</p>

<pre class="brush: js">window.onfocus();
</pre>

<p>Une erreur faite souvent lorsque l'on commence à utiliser JavaScript est d'ajouter des parenthèses et/ou des paramètres à la fin de la variable. Cela revient à appeler le gestionnaire d'événement lorsqu'on l'assigne. Le fait d'ajouter ces parenthèses assignera la valeur de retour du gestionnaire d'événement. Cette valeur sera souvent<code> undefined </code>dans ces cas alors que l'on aurait souhaité obtenir le gestionnaire d'événement.</p>

<pre class="brush: js">document.form1.button1.onclick = setBGColor();
</pre>

<p>Afin de passer des paramètres à un gestionnaire d'événements, le gestionnaire doit être enveloppé dans une autre fonction, comme dans l'exemple suivant :</p>

<pre class="brush: js">document.form1.button1.onclick = function() {
   setBGColor('une valeur');
};
</pre>

<h2 id="Les_fonctions_de_bloc">Les fonctions de bloc</h2>

<p>En <a href="/fr/docs/Web/JavaScript/Reference/Strict_mode">mode strict</a>, à partir d'ES2015 (ES6), la portée des fonctions définies dans un bloc est limitée à ce bloc. Avant ES2015, il était interdit d'utiliser les fonctions de bloc en mode strict..</p>

<pre class="brush: js">'use strict';

function f() {
  return 1;
}

{
  function f() {
    return 2;
  }
}

f() === 1; // true

// f() === 2 en mode non-strict
</pre>

<h3 id="Les_fonctions_de_bloc_dans_du_code_non-strict">Les fonctions de bloc dans du code non-strict</h3>

<p>Non.</p>

<p>Dans du code non-strict, les déclarations de fonctions placées dans des blocs peuvent se comporter de façon étrange :</p>

<pre class="brush: js">if (onDevraitDéfinirZéro) {
   function zéro() { // DANGER: risque de compatibilité
      console.log("Voici zéro.");
   }
}
</pre>

<p>ES2015 indique que si <code>onDevraitDéfinirZéro</code> vaut <code>false</code>, <code>zéro</code> ne devrait jamais être défini car le bloc n'est jamais exécuté. En revanche, c'est une nouveauté liée à cette version du standard, non spécifiée auparavant. Certains navigateurs définissent <code>zéro</code> que le bloc soit exécuté ou non.</p>

<p>En <a href="/fr/docs/Web/JavaScript/Reference/Strict_mode">mode strict</a>, tous les navigateurs qui prennent en charge ES2015 gère cela de la même façon : <code>zéro</code> est uniquement défini si <code>onDevraitDéfinirZéro</code> vaut <code>true</code> et uniquement dans la portée du bloc induit par <code>if</code>.</p>

<p>Une méthode plus sûre est d'utiliser des expressions de fonction :</p>

<pre class="brush: js">var zéro;
if (0) {
   zéro = function() {
      console.log("Voici zéro.");
   };
}
</pre>

<h2 id="Exemples_2">Exemples</h2>

<h3 id="Renvoyer_un_nombre_formaté">Renvoyer un nombre formaté</h3>

<p>La fonction qui suit renvoie une chaîne de caractères contenant la représentation formatée d'un nombre avec un certain nombre de zéros préfixant le nombre.</p>

<pre class="brush: js">// Cette fonction renvoie une chaîne de caractères complétée par un préfixe composé de zéros
function padZeros(num, totalLen) {
   var numStr = num.toString();             // On initialise la valeur à renvoyer en chaîne de caractères
   var numZeros = totalLen - numStr.length; // On calcule le nombre de zéros
   for (var i = 1; i &lt;= numZeros; i++) {
      numStr = "0" + numStr;
   }
   return numStr;
}
</pre>

<p>Les instructions qui suivent utilisent cette fonction</p>

<pre class="brush: js">var resultat;
resultat = padZeros(42,4); // renvoie "0042"
resultat = padZeros(42,2); // renvoie "42"
resultat = padZeros(5,4);  // renvoie "0005"
</pre>

<h3 id="Déterminer_si_une_fonction_existe">Déterminer si une fonction existe</h3>

<p>Il est possible de déterminer si oui ou non une fonction existe en utilisant l'opérateur <code>typeof</code>. Dans l'exemple qui suit, on teste pour savoir si l'objet<code> window</code> possède une propriété appelé <code>noFunc</code> qui serait une fonction. Si c'est le cas, elle sera utilisée, sinon on fera autre chose.</p>

<pre class="brush: js"> if ('function' === typeof window.noFunc) {
   // utilisation de noFunc()
 } else {
   // faire autre chose
 }
</pre>

<p>Il est à noter que, dans le test <code>if</code>, on utilise une référence à <code>noFunc</code> - il n'y a pas de parenthèses après le nom de la fonction, la fonction n'est donc pas appelée.</p>

<h2 id="Spécifications">Spécifications</h2>

<table class="standard-table">
 <tbody>
  <tr>
   <th scope="col">Spécification</th>
   <th scope="col">État</th>
   <th scope="col">Commentaires</th>
  </tr>
  <tr>
   <td>{{SpecName('ES1')}}</td>
   <td>{{Spec2('ES1')}}</td>
   <td>Définition initiale. Implémentée avec JavaScript 1.0</td>
  </tr>
  <tr>
   <td>{{SpecName('ES5.1', '#sec-13', 'Function Definition')}}</td>
   <td>{{Spec2('ES5.1')}}</td>
   <td></td>
  </tr>
  <tr>
   <td>{{SpecName('ES6', '#sec-function-definitions', 'Function definitions')}}</td>
   <td>{{Spec2('ES6')}}</td>
   <td>Nouveautés : fonctions fléchées, générateurs, paramètres par défaut, paramètres du reste</td>
  </tr>
  <tr>
   <td>{{SpecName('ES6', '#', 'function*')}}</td>
   <td>{{Spec2('ES6')}}</td>
   <td>Définition initiale.</td>
  </tr>
  <tr>
   <td>{{SpecName('ES6', '#sec-arrow-function-definitions', 'Arrow Function Definitions')}}</td>
   <td>{{Spec2('ES6')}}</td>
   <td>Définition initiale.</td>
  </tr>
 </tbody>
</table>

<h2 id="Compatibilité_des_navigateurs">Compatibilité des navigateurs</h2>

<p>{{Compat("javascript.functions")}}</p>

<h2 id="Voir_aussi">Voir aussi</h2>

<ul>
 <li>L'instruction {{jsxref("Instructions/function", "function")}}</li>
 <li>L'expression {{jsxref("Opérateurs/L_opérateur_function", "function")}}</li>
 <li>L'instruction {{jsxref("Instructions/function*", "function*")}}</li>
 <li>L'expression {{jsxref("Opérateurs/function*", "function*")}}</li>
 <li>{{jsxref("Function")}}</li>
 <li>{{jsxref("GeneratorFunction")}}</li>
 <li>{{jsxref("Fonctions/Fonctions_fléchées", "Les fonctions fléchées")}}</li>
 <li>{{jsxref("Fonctions/Valeurs_par_défaut_des_arguments", "Les paramètres par défaut","",1)}}</li>
 <li>{{jsxref("Fonctions/paramètres_du_reste", "Les paramètres du reste","",1)}}</li>
 <li>L'objet {{jsxref("Fonctions/arguments", "arguments")}}</li>
 <li>{{jsxref("Fonctions/get", "getter")}}</li>
 <li>{{jsxref("Fonctions/set", "setter")}}</li>
 <li>{{jsxref("Fonctions/Définition_de_méthode", "Les définitions de méthodes","",1)}}</li>
 <li><a href="/fr/docs/Web/JavaScript/Reference/Fonctions">Fonctions et portée des fonctions</a></li>
</ul>