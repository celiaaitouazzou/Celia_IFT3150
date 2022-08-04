## Semaine 9-10 : semaine du 4 juillet et semaine du 15 juillet

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
<li>Ressources consultés durant cette étape: <br>
	<ul>
		<li><a href="https://www.w3schools.com/js/js_json_parse.asp">https://www.w3schools.com/js/js_json_parse.asp</a></li>
		<li><a href="https://www.pluralsight.com/guides/convert-strings-to-json-objects-in-javascript-with-eval">https://www.pluralsight.com/guides/convert-strings-to-json-objects-in-javascript-with-eval</a></li>
		<li><a href="https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce">https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce</a></li>
		<li><a href="https://stackoverflow.com/questions/52281389/convert-xml-to-json-with-nodejs">https://stackoverflow.com/questions/52281389/convert-xml-to-json-with-nodejs</a></li> 
		<li><a href="https://www.w3schools.com/js/js_json_parse.asp">https://www.w3schools.com/js/js_json_parse.asp</a></li>
		<li><a href="https://github.com/nashwaan/xml-js">https://github.com/nashwaan/xml-js</a> </li>
		<li><a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element#svg_and_mathml">https://developer.mozilla.org/en-US/docs/Web/HTML/Element#svg_and_mathml</a></li>
	</ul>
</li>

<li>Finalement, on est arrivé à cette librairie qui converti xml en objet (fxp library):<li><a href="https://www.npmjs.com/package/fxp">https://www.npmjs.com/package/fxp</a></li>
<li> 22eb4ade6b1ed0808592fb9526b21288e1a2b958 : J'ai commencé un premier algorithme qui traversait les éléments d'un objet et si l'élément avait plus d'un enfant alors rappeler la fonction récursivement. <b>On tente d'accumuler les éléments de l'arbre XML dans la liste a</b> , un paramètre de la function. <br>
Ressource Utilisée pour cette étape: 
<ul>
	<li><a href="https://stackoverflow.com/questions/5223/length-of-a-javascript-object">https://stackoverflow.com/questions/5223/length-of-a-javascript-object</a></li>
	<li><a href="https://stackoverflow.com/questions/455338/how-do-i-check-if-an-object-has-a-key-in-javascript">https://stackoverflow.com/questions/455338/how-do-i-check-if-an-object-has-a-key-in-javascript</a> </li>
	<li><a href = "https://stackoverflow.com/questions/126100/how-to-efficiently-count-the-number-of-keys-properties-of-an-object-in-javascript">https://stackoverflow.com/questions/126100/how-to-efficiently-count-the-number-of-keys-properties-of-an-object-in-javascript</a></li>
	<li><a href="https://www.educative.io/answers/how-to-get-keys-values-and-entries-in-javascript-object">https://www.educative.io/answers/how-to-get-keys-values-and-entries-in-javascript-object</a></li>
	<li>Cela pour traverser récursivement le JSON : <a href="https://stackoverflow.com/questions/4104321/recursively-parsing-json">https://stackoverflow.com/questions/4104321/recursively-parsing-json</a></li>
	
</ul>
</li>
<li>
	On a essayé la même chose qu'à la précédente itération , mais à la place que a soit un paramètre , a est une variable de liste vide , mais à chaque appel récursif , cela vidait la liste , alors cela n'était pas la solution 
</li>
<li>
	0fd1cb624b350d2c0d3ea93ca04fb304a70a8e46 : J'ai essayé d'accumuler les éléments de l'arbre xml dans la liste a avec la fonction <it>Reduce</it> pour ensuite enlever les doublons via : <a href="https://stackoverflow.com/questions/2218999/how-to-remove-all-duplicates-from-an-array-of-objects">https://stackoverflow.com/questions/2218999/how-to-remove-all-duplicates-from-an-array-of-objects</a> , ou les ajouter puis s'ils sont là , les enlever de la liste de concept ,ce qui me donnait une erreur , alors pour tenter de règler le problème , j'ai consulté  : <a href="https://stackoverflow.com/questions/5767325/how-can-i-remove-a-specific-item-from-an-array">https://stackoverflow.com/questions/5767325/how-can-i-remove-a-specific-item-from-an-array</a>,<a href="https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array/splice">https://stackoverflow.com/questions/5767325/how-can-i-remove-a-specific-item-from-an-array</a>. Mais cela n'a pas marché alors nous avons abandonné la solution.

<li><b>Note important pour plus tard à la fois pour les yml plus complexe (embriqués) et le xml :</b><a href="https://stackoverflow.com/questions/2549320/looping-through-an-object-tree-recursively">https://stackoverflow.com/questions/2549320/looping-through-an-object-tree-recursively</a></li>

<li>Nous avons finalement réussi à accumuler les éléments dans une liste , mais nous avons découvert l'objet DOMParser qui nous permet de traverser l'arbre XML plus efficacement et donc de parser plus efficacement que si on devait raffiner une liste fonction après fonction. (Voir semaine 11-12 pour voir comment j'ai fait ) </li>
<li>
	Ressources utilisés pour cette étape : 
	<ul>
		<li><a href = "https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Classes/constructor">https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Classes/constructor</a></li>
		<li><a href = "https://linuxhint.com/convert-object-to-string-javascript/">https://linuxhint.com/convert-object-to-string-javascript/</a></li>
		<li><a href = "https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Object/keys"> https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Object/keys</a></li>
	</ul>
</li>



commencer à travailler sur le rapport d'avancement et rapport synthèse, les tests, le nettoyage

- 


- https://www.npmjs.com/package/chai
- https://www.npmjs.com/package/mocha?activeTab=versions
- 