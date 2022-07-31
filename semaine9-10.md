## Semaine 9-10 : semaine du 4 juillet

### Fin de la conversion du YML 

<ul>Cette semaine on a complété le yml . Ce qui fait qu'on a ajouté les fonctions : 
	<li>findSimilarities : prend l'objet yml original et retourne un dictionnaire où les clefs sont toutes les clefs différentes de l'objet et les valeurs sont des listes vides</li>
	<li>refineSimilarities() : 
		<ul>
			<li>appelle findSimilarities() et le met dans la variable allAttribute</li>
			<li>On itère à travers les concepts de la liste de concept qu'on a généré précédemment , puis on accède à la liste d'attributs de chaque concept et pour chaque attribut, ajoute, si pas déjà fait , dans l'array  qui est la valeur d'une clé , de allAttributele contenu en string de l'attribut et par la même instance l'ajoute à l'array qui contient les attributs en question.</li>
			<li>retourne une array où le premier élément est le dictionnaire  = allAttribute dûement rempli et le deuxième élément est la liste d'attributs en questions qu'on a mentionné précedemment.</li>
			<li>On va l'utiliser pour différents context plus tard.</li>
		</ul>
	</li>
	<li>eliminateDoublons() : Quand une valeur d'une clé de refineSimilarities complet a deux éléments ou plus pareil ,cela fait qu'on juste les éléments différents. </li>
	<li>eliminateRequired(): 
		<ul>
			<li>appelle eliminateDoublons()</li>
			<li>on itère à travers le dictionnaire complet et pour chaque nom d'attribut , on le cherche dans la liste de concept et s,Il y a un concept qui l'a et qu'il y a plus d,une version de l'attribut et que required = true (la seule différence entre deux attributs de même nom est le required) alors on mets le required à true </li>
			<li>On appelle findDifferentConcepts, si cela fait que deux concepts sont identiques, supprimer celui en trop</li>
		</ul>
	</li>
	<li>getPrototypeConcept() : appelé SEULEMENT si après eliminateRequired() , il y a plus d'un concept dans la liste
		<ul>
			<li>On instancie un nouveau concept qui sera le prototype du yml</li>
			<li>si dans tous les concepts , un certain attribut est pareil partout dans tous les concepts , on l'inclut à la liste d'attribut du prototype.</li>
			<li>on fait qu'il y ait un exemplaire de chaque attribut comme à eliminateDoublons()</li>
			<li>On retourne le prototype </li>
		</ul>
	</li>
	<li>getProtoAttributeName() : accumule les noms d'attributs dans une liste et la retourne.</li>
	<li>updateConceptList() : On itère à travers les concepts et pour chaque concept , on itère à travers sa liste d'attribut et si la liste de nom d'attributs du prototype == nom d'attribut dans la liste de concept alors , on supprime l'attribut dans la liste de concept.
	</li>
	<li>add_prototype : ajoute le concept prototype à la liste de concept</li>
	<li>main() : appelle les fonctions dans l'ordre pour convertir l'object yml en object ConceptList par lequel on peut just faire JSON.stringify(objetConceptList) et avoir notre JSON en bonne et dûe forme: 
<p>
	main()
{
this.generateConceptList();
this.findDifferentConcepts();
this.eliminateRequired();


if(this.listConcept.length > 1)
{
    this.updateConceptList();
    this.add_prototype(); 
}
this.nameTheConcepts();
}
</p>
	</li>
	<li>On a fini 99% du yml , il reste à tester avec plus d'exemple et  les optimisations possibles du code à faire.<li>
	<li>Liens utilisés : 
		<ul>
			<li><a href = "https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array/find#sp%C3%A9cifications"></a>https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array/find#sp%C3%A9cifications</li>
			<li><a href="https://benyoss4.medium.com/what-is-js-subclassing-and-how-its-a-time-saver-be46995c95ce"></a>https://benyoss4.medium.com/what-is-js-subclassing-and-how-its-a-time-saver-be46995c95ce</li>
			<li><a href ="https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Classes/extends">https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Classes/extends</a></li>
		</ul>
	</li>
</ul>

### Début de la conversion du XML 

<li>D'abord , comme d'habitude parser le document xml en object </li>
<li> On a essayé plusieurs librairie npm avant de trouver la bonne notamment : 
	<li>D'abord on a essayé la librairie fast XML Parser : <a href="https://www.npmjs.com/package/fast-xml-parser">https://www.npmjs.com/package/fast-xml-parser</a> résultat pas marché. On ne trouvait pas le module quand on faisait require.
<li>On a essayé: <a href="https://www.npmjs.com/package/xml-parser">https://www.npmjs.com/package/xml-parser</a> Résultat : installation marche mais quand on l'essaie sur bibliotheque.xml cela donne : {
  declaration: { attributes: { version: '1.0', encoding: 'UTF-8' } },
  root: undefined} , ce qui n'est pas du tout ce que nous rechechons.</li>

<li>On essaie ensuite <a href="https://www.npmjs.com/package/xml-parse">https://www.npmjs.com/package/xml-parse</a>. On avait juste la couche extérieure et il aurait fallu implémenter une logique récursive de on rentre dans innerXML qu'on parse pour ensuite itérer à travers ses élément et encore avoir une string appelé innerHTML pour avoir un objet utilisable dans le futur. </li>

<li>Ensuite, on a essayé la librairie : <a href="https://www.npmjs.com/package/dom-parser">https://www.npmjs.com/package/dom-parser</a> 
et j'ai appris que cela existait via <a href="https://medium.com/@nitinpatel_20236/converting-xml-to-json-using-recursion-7b1df91b42d8">https://medium.com/@nitinpatel_20236/converting-xml-to-json-using-recursion-7b1df91b42d8</a>.Par la suite , on a suivi la fonction xml2json(srcDOM) est directement prise de : <a href="https://medium.com/@nitinpatel_20236/converting-xml-to-json-using-recursion-7b1df91b42d8">https://medium.com/@nitinpatel_20236/converting-xml-to-json-using-recursion-7b1df91b42d8</a> mais il y avait des problèmes avec la ligne let children = [...srcDOM.children]; qui me donnait une erreur que le string en xml qu'on essaie de convertir n'est pas un itérable alors on ne peut pas le faire donc on ne garde pas cette idée ni la fonctiopn xml2json(srcDOM)<. Alors j'ai abandonné la tentative au complet. </li>

<li>On est revenu avec la première librairie et avec les solutions suivantes , on essaies de débogguer l'import de la librairie:<a href="https://stackoverflow.com/questions/9023672/how-do-i-resolve-cannot-find-module-error-using-node-js">https://stackoverflow.com/questions/9023672/how-do-i-resolve-cannot-find-module-error-using-node-js</a>,<a href="https://stackoverflow.com/questions/19272880/node-js-require-and-module-not-found">https://stackoverflow.com/questions/19272880/node-js-require-and-module-not-found</a>, on aussi essayé d'appeler fast xml en téléchargeant le github de fast xml <a href="https://github.com/NaturalIntelligence/fast-xml-parser">https://github.com/NaturalIntelligence/fast-xml-parser</a> et on a tenté de require les fichiers qui font l'import avec :<a href="https://attacomsian.com/blog/nodejs-check-if-directory-exists">https://attacomsian.com/blog/nodejs-check-if-directory-exists</a> .Elle ne sera pas retenue pour être utilisée ,car rien de tout cela a marché pour convertir le xml en objet.</li>

<li>Pour voir comment je peux règler l'erreur avec la librairie en question.</li>
<li>Finalement, on est arrivé à faire marcher la librairie:<li><a href="https://www.npmjs.com/package/fxp">https://www.npmjs.com/package/fxp</a> On a utilisé ce repertoire pour pouvoir faire l'import et on appelle fxp.js à partir de require </li>
<li>On tente de récursivement passer à travers l'arbre XML et ceci m'aide avec la récursivité<a href="https://stackoverflow.com/questions/5223/length-of-a-javascript-object">https://stackoverflow.com/questions/5223/length-of-a-javascript-object</a>.Puis itérerer à travers un objet et l'accumuler dans une data structure (j'ai essayé d'accumuler cela dans un objet comme JSON et j'ai essayé avec une liste ) tout en faisant la récursion mais souvent on a 'can't push on undefined'. Et ce fut notre problème pendant  une semaine . Pour des raisons que je ne sais pas , la liste devenait undefined et bien sûr quand j'essaiyais de push dans une list undefined , cela générait une erreur. J'ai essayé d'en faire une variable , mais quand je rappelais la fonction , naturellement, elle redevenait vide, j'ai essayé d'en faire un attribut de la classe YMLParserSerializer mais cela ne marchait pas. J'ai également essayé d'utiliser cela <a href="https://www.w3schools.com/js/js_json_parse.asp">https://www.w3schools.com/js/js_json_parse.asp</a> et <a href="https://www.pluralsight.com/guides/convert-strings-to-json-objects-in-javascript-with-eval">https://www.pluralsight.com/guides/convert-strings-to-json-objects-in-javascript-with-eval</a>pour faire du xml en string ou en object en un JSON en accumulant comme j'avais dit puis ensuite traiter le JSON, comme j'ai traité le yml . Mais ni l'accumulation des éléments dans une liste ni dans un json n'a marché.Finalement la solution désirée est de convertir la string xml en json ce que ce code fait très bien et c'est cette solution qui est sélectionnée pour l'instant:<a href="https://stackoverflow.com/questions/52281389/convert-xml-to-json-with-nodejs">https://stackoverflow.com/questions/52281389/convert-xml-to-json-with-nodejs</a>.Voici la librairie en question : <a href="https://github.com/nashwaan/xml-js">https://github.com/nashwaan/xml-js</a> J'ai également lu la documentation de la librairie qui a converti le xml en yml</li>. Mais nous avions le même problème une fois que cela était converti en json avec la récursion jusqu'à ce que je ce j'ajoute une ligne de code vendredi 15 juillet en faisant que je ne fasse plus d'appel récursif. J'ai réussi à récupérer les éléments de l'arbre XML dans une liste , mais à ce moment , Louis-Édouard m'a recommandé d'utiliser l'objet Dom Parser puis utiliser les méthodes de cet objet car ce sera plus facile et plus efficace. 
<li><b>Note important pour plus tard à la fois pour les yml plus complexe (embriqués) et le xml :</b><a href="https://stackoverflow.com/questions/2549320/looping-through-an-object-tree-recursively">https://stackoverflow.com/questions/2549320/looping-through-an-object-tree-recursively</a></li>
<li></li>


<li><a href="https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce">https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce</a> Plus de ressources utiles </li>
<li><a href="https://developer.mozilla.org/fr/docs/Web/API/DOMParser">https://developer.mozilla.org/fr/docs/Web/API/DOMParser</a>Utilisé pour une précédente itération pour convertir xml en json </li>
<li><a href="https://www.w3schools.com/js/js_json_parse.asp">https://www.w3schools.com/js/js_json_parse.asp</a></li>
<li><a href="https://www.npmjs.com/package/dom-parser">https://www.npmjs.com/package/dom-parser</a>Librairie finalement utilisé</li>
<li><a href="https://www.w3schools.com/jsref/prop_node_firstchild.asp">https://www.w3schools.com/jsref/prop_node_firstchild.asp</a> </li>
<li><a href="https://www.w3schools.com/xml/dom_nodes_access.asp">https://www.w3schools.com/xml/dom_nodes_access.asp</a></li>
<li><a href="https://www.w3schools.com/xml/dom_nodes_access.asp">https://www.w3schools.com/xml/dom_nodes_access.asp</a></li>

<li><a href="https://github.com/xmldom/xmldom">https://github.com/xmldom/xmldom</a></li>
<li><a href="https://developer.mozilla.org/en-US/docs/Web/API/DOMParser">https://developer.mozilla.org/en-US/docs/Web/API/DOMParser</a></li>
<li><a href="https://developer.mozilla.org/en-US/docs/Web/API/Document">https://developer.mozilla.org/en-US/docs/Web/API/Document</a></li>
<li><a href="https://www.npmjs.com/package/dom-parser">https://www.npmjs.com/package/dom-parser</a>Librairie finalement utilisé</li>
<li><a href="https://www.w3schools.com/jsref/prop_node_firstchild.asp">https://www.w3schools.com/jsref/prop_node_firstchild.asp</a> </li>
<li><a href="https://www.w3schools.com/xml/dom_nodes_access.asp">https://www.w3schools.com/xml/dom_nodes_access.asp</a></li>
<li><a href="https://www.javascripttutorial.net/javascript-dom/javascript-get-child-element/">https://www.javascripttutorial.net/javascript-dom/javascript-get-child-element/</a></li>
<li><a href="https://attacomsian.com/blog/javascript-dom-check-if-an-element-has-children">https://attacomsian.com/blog/javascript-dom-check-if-an-element-has-children</a></li>

<li><a href="https://www.w3schools.com/jsref/prop_node_firstchild.asp">https://www.w3schools.com/jsref/prop_node_firstchild.asp</a></li>
<li><a href="https://developer.mozilla.org/fr/docs/Web/API/Document/documentElement">https://developer.mozilla.org/fr/docs/Web/API/Document/documentElement</a> </li>
<li><a href="https://www.javascripttutorial.net/javascript-dom/javascript-get-child-element/">https://www.javascripttutorial.net/javascript-dom/javascript-get-child-element/</a></li>
<li><a href="https://attacomsian.com/blog/javascript-dom-check-if-an-element-has-children">https://attacomsian.com/blog/javascript-dom-check-if-an-element-has-children</a></li>
<li><a href="https://developer.mozilla.org/fr/docs/Web/API/Element/hasAttribute">https://developer.mozilla.org/fr/docs/Web/API/Element/hasAttribute</a> </li>
<li><a href="https://developer.mozilla.org/fr/docs/Web/API/Element/attributes">https://developer.mozilla.org/fr/docs/Web/API/Element/attributes</a></li>
<li><a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element#svg_and_mathml">https://developer.mozilla.org/en-US/docs/Web/HTML/Element#svg_and_mathml</a></li>

- https://www.w3schools.com/jsref/prop_node_firstchild.asp
- https://developer.mozilla.org/fr/docs/Web/API/Document/documentElement
- https://www.javascripttutorial.net/javascript-dom/javascript-get-child-element/
- https://attacomsian.com/blog/javascript-dom-check-if-an-element-has-children
- https://developer.mozilla.org/fr/docs/Web/API/Element/hasAttribute
- https://developer.mozilla.org/fr/docs/Web/API/Element/attributes
- https://developer.mozilla.org/en-US/docs/Web/HTML/Element#svg_and_mathml
- https://attacomsian.com/blog/javascript-dom-get-the-parent-of-an-element
- https://www.w3schools.com/jsref/prop_element_childelementcount.asp
- https://www.w3schools.com/colors/colors_picker.asp
- https://www.freecodecamp.org/news/check-if-javascript-array-is-empty-or-not-with-length/

commencer à travailler sur le rapport d'avancement et rapport synthèse, les tests, le nettoyage

- https://stackoverflow.com/questions/2218999/how-to-remove-all-duplicates-from-an-array-of-objects
- https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach
- https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce
- https://stackoverflow.com/questions/455338/how-do-i-check-if-an-object-has-a-key-in-javascript
- https://stackoverflow.com/questions/455338/how-do-i-check-if-an-object-has-a-key-in-javascript
- https://stackoverflow.com/questions/5767325/how-can-i-remove-a-specific-item-from-an-array
- https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array/splice
- https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Classes/constructor
- https://stackoverflow.com/questions/126100/how-to-efficiently-count-the-number-of-keys-properties-of-an-object-in-javascrip
- https://www.educative.io/answers/how-to-get-keys-values-and-entries-in-javascript-object
- https://linuxhint.com/convert-object-to-string-javascript/
- https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Object/keys
- https://stackoverflow.com/questions/4104321/recursively-parsing-json
- https://www.npmjs.com/package/chai
- https://www.npmjs.com/package/mocha?activeTab=versions
- 