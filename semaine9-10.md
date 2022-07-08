## Semaine 9 et 10 : import 

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
</ul>