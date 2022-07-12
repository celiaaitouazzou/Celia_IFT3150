## Semaine 9 et 10 : import 

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
<li>D'abord on a essayé la librairie : <a href="https://www.npmjs.com/package/fast-xml-parser">https://www.npmjs.com/package/fast-xml-parser</a> résultat pas marché</li>
<li>On a essayé: <a href="https://www.npmjs.com/package/xml-parser">https://www.npmjs.com/package/xml-parser</a> Résultat : installation marche mais quand on l'essaie sur bibliotheque.xml cela donne : {
  declaration: { attributes: { version: '1.0', encoding: 'UTF-8' } },
  root: undefined
} , ce qui n'est pas du tout ce que nous rechechons</li>
<li>On essaie ensuite <a href="https://www.npmjs.com/package/xml-parse">https://www.npmjs.com/package/xml-parse</a> Résultat : on avait juste la couche extérieure et il aurait fallu implémenter une logique récursive de on rentre dans innerXML qu'on parse pour ensuite itérer à travers ses élément et encore avoir un innerHTML pour avoir un objet utilisable dans le futur</li>
<li>Essaie 4 : <a href="https://www.npmjs.com/package/dom-parser">https://www.npmjs.com/package/dom-parser</a> 
et j'ai appris que cela existait via <a href="https://medium.com/@nitinpatel_20236/converting-xml-to-json-using-recursion-7b1df91b42d8">https://medium.com/@nitinpatel_20236/converting-xml-to-json-using-recursion-7b1df91b42d8</a></li>
<li>la fonction xml2json(srcDOM) est directement prise de : <a href="https://medium.com/@nitinpatel_20236/converting-xml-to-json-using-recursion-7b1df91b42d8">https://medium.com/@nitinpatel_20236/converting-xml-to-json-using-recursion-7b1df91b42d8</a></li>
<li>On essait cette méthode et on a une erreur que le string en xml qu'on essaie de convertir n'est pas un itérable alors on ne peut pas le faire donc on ne garde pas cette idée ni la fonctiopn xml2json(srcDOM)</li>
<li>On est revenu avec la première librairie et avec du déboggage de stack et en essayant tous ces sites , on est arrivé à faire marcher la librairie: 
	<ul>
		


	
<li><a href="https://www.npmjs.com/package/fxp">https://www.npmjs.com/package/fxp</a>Consulter dans le but de débogger pour utiliser fast-xml-parser</li>
<li><a href="https://stackoverflow.com/questions/9023672/how-do-i-resolve-cannot-find-module-error-using-node-js">https://stackoverflow.com/questions/9023672/how-do-i-resolve-cannot-find-module-error-using-node-js</a>Encore une fois déboggage la librarie pour qu'on puisse l'utiliser</li>
<li><a href="https://stackoverflow.com/questions/9023672/how-do-i-resolve-cannot-find-module-error-using-node-js">https://stackoverflow.com/questions/9023672/how-do-i-resolve-cannot-find-module-error-using-node-js</a>Autre déboggage du modules</li>
<li><a href="https://stackoverflow.com/questions/19272880/node-js-require-and-module-not-found">https://stackoverflow.com/questions/19272880/node-js-require-and-module-not-found</a>Pour voir comment je peux règler l'erreur avec la librairie en question.</li>
<li><a href="https://github.com/NaturalIntelligence/fast-xml-parser">https://github.com/NaturalIntelligence/fast-xml-parser</a> On a utilisé ce repertoire pour pouvoir faire l'import et on appelle fxp.js à partir de require </li>
<li><a href="https://attacomsian.com/blog/nodejs-check-if-directory-exists">https://attacomsian.com/blog/nodejs-check-if-directory-exists</a>Pour checker si mon directory que j'appelle dans require est valide</li><li><a href="https://www.npmjs.com/package/fast-xml-parser">https://www.npmjs.com/package/fast-xml-parser</a> Apprend la base de comment utiliser le parser </li>
<li><a href="https://stackoverflow.com/questions/5223/length-of-a-javascript-object">https://stackoverflow.com/questions/5223/length-of-a-javascript-object</a> M'aide avec la récursivité</li>
<li><a href="https://stackoverflow.com/questions/5223/length-of-a-javascript-object">https://stackoverflow.com/questions/5223/length-of-a-javascript-object</a>Utilisé pour une précédente itération pour convertir xml en json </li>
<li><a href="https://www.w3schools.com/js/js_json_parse.asp">https://www.w3schools.com/js/js_json_parse.asp</a>Également utilsé pour une préceédente itération dans un code pour convertir xml en structure utilisable  </li>
<li><a href="https://www.pluralsight.com/guides/convert-strings-to-json-objects-in-javascript-with-eval">https://www.pluralsight.com/guides/convert-strings-to-json-objects-in-javascript-with-eval</a> Aussi utilisé pour une ancienne itération où on visait directment convertir xml en json</li>
<li><a href="https://stackoverflow.com/questions/52281389/convert-xml-to-json-with-nodejs">https://stackoverflow.com/questions/52281389/convert-xml-to-json-with-nodejs</a> Finalement la solution désirée est de convertir la string xml en json ce que ce code fait très bien et c'est cette solution qui est sélectionnée</li>
<li><a href="https://github.com/nashwaan/xml-js">https://github.com/nashwaan/xml-js</a> Lue la documentation de la librairie qui a converti le xml en yml </li>
<li><a href="https://stackoverflow.com/questions/2549320/looping-through-an-object-tree-recursively">https://stackoverflow.com/questions/2549320/looping-through-an-object-tree-recursively</a><b>Très important : À retenir à la fois pour les yml plus complexe et le xml.</b></li>
</ul>
</li>