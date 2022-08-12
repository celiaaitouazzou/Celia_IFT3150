## Semaine 13-14 : Import 


### August 4 2022 : Tests

<p>Le nettoyage a été fait. Maintenant il reste les test et finaliser gentleman, le rapport des activités, le rapport technique.</p>
<ul>
	<li>On commence par les tests. On télécharge d'abord les package de test notamment : <a href="https://www.npmjs.com/package/chai">https://www.npmjs.com/package/chai</a>,<a href= "https://www.npmjs.com/package/mocha?activeTab=versions">https://www.npmjs.com/package/chai</a>,<a href="https://www.chaijs.com/api/bdd/#method_all">https://www.chaijs.com/api/bdd/#method_all</a></li>
	<li>
		On commence par tester le csv ce qui inclut:
		<ul>
			<li>Node n'arrivait pas à reconnaître describe et nous en avions besoin donc on a fait un refactoring massif en bougeant converter-csv.js à /src/importer et modifier package.json pour que les tests fonctionnent avec notre fichier de test </li>
			<li>On refactor le code de sorte à ce que au lieu qu'on appelle une classe. Au lieu d'une classe , nous avons un objet(dictionnaire), contenant les fonctions et les attributs. On crée un objet indépendant via function qu'on appelle afin d'instancier un objet et faire des manoeuvres sur lui.</li>
			<li>On a d'abord commencé par un premier test: celui de la fonction file2DDataFrame. On a vu si on donnait cette fonction un object CSVParserSerializer valide, il nous retournerait une array, sinon il nous retourne une erreur. Les tests de ces deux cas ont passés.</li>
			<li>Ensuite , nous sommes passé à la fonction execute , voici les fonctionnalité à tester (aka. ce que la fonction doit absolument faire avec succès pour toutes ses inputs ) : 
				<ul>
					<li>D'abord il faut tester que si on a un csv non-valide , on aura le message d'erreur , dans les cas suivant  :
						<ul>
							<li>L'entête a plus d'éléments que les lignes d'entrées.</li>
							<li>L'entête a moins d'éléments que les lignes d'entrées.</li>
							<li>Une ligne a plus d'élément que l'entête.</li>
							<li>Une ligne a moins d'éléments que l'entête</li>
						</ul> 
						<li>Cela par la même occasion vérifie si la fonction validation marche. </li>
					</li>
					<li>Si on a un csv-valide  , on: 
						<ul>
							<li>Crée un concept "collection_de_rangee", alors vérifier que cela est bien le cas </li>
							<li>Vérifier que c'est bien un concept concret</li>
							<li>Vérifier qu'il a juste un seul attribut</li>
							<li>Vérifier que cette attribut n'est pas null</li>
							<li>Vérifier qu'il s'agit d'un attribut de target "set"</li>
							<li>Vérifier que le target a un accept</li>
							<li>Vérifier que le nom du accept correspond au nom du second concept</li>
							<li>Vérifier que le nombre d'attribut du second concept <b>dites concept Entête</b>, correspond au nombre de colonne de l'entête</li>
							<li>Vérifier que les noms de colonnes correspondent au noms des attributs</li>
							<li>Vérifier que la fonction createAttributefromDataFrame(dataframe) crée une array avec autant d'élément que l'entête</li>
							<li>Vérifier que la fonction createAttributefromDataFrame(dataframe) crée une array avec les bons éléments pour une liste vide, une liste avec un élément et une liste avec plusieurs éléments. </li>
							<li></li>
							<li>Vérifier que tous les attributs de l'entête correspondent à exactement un nom d'attribut de la liste du concept Entête</li>
						</ul>
					</li>
				</ul>
			</li>
			<li>Cela conclut les tests pour l'import du csv.</li>
		</ul>
	</li>
	<li>On continue avec le test du yml ce qui inclut: 
		<ul>
			<li>Faire la refactorisation du code tel que nous l'avons fait pour le csv i.e. transformer les fonctions et les classes en objets appellable.(Fait)</li>
			<li>D'abord, on appelle yml2JsonObject(readAfile(filename)), ce qui retourne un objet Json si le fichier existe et qu'il est convertible en objet Json , sinon , il retourne un message d'erreur. On test ces deux cas avec deux tests.</li>
			<li>On le met dans une variable v</li>
			<li>Ensuite on test la fonction this.recursiveFetchAttribute(jsonObject,createConcept(th.conceptName,"concrete",[]),{}) et nous aurons alors les cas de tests suivants: 
				<ul>
					<li>Cette fonction accepte 3 type d'élément : une array , un objet , une paire (clé valeur).</li>
					<li>On va tester si on a null, tel qu'on a un objet {a:3,b:4, null, c:5 }, je ne sais pas ce que nous ferions parce que ce cas n'est pas prévu dans le code. <b> À faire : Nous verrons comment implémenter cette logique dans le code. </b> </li>
					<li>Par ailleurs , cela \"a\":1 devrait retourner une erreur puisqu'il n'y a pas d'espace entre "a":1</li>
					<li>Mais "a:1" devrait marcher mais retourner un liste de concept vide.</li>
					<li>Vérifier que Cela devrait retourner "a: 1,b: 2" une erreur.Vérifier que cela devrait retourner une liste non-vide de concepts avec un seul attribut a dans un seul concept "concept" qui a une valeur string et un attribut required.</li>
					<li>Vérifier que cela "\"a\":1,b:2" ne devrait pas marcher. Cela ne marche pas pour les même raisons que "a":1 ne marche pas.</li>
					<ul>
					<li><b>Update du 11 août 2022 : </b> J'ai réaliser que generateConceptList(conceptObject) qui prend l'objet de concept et génère la liste de concept à partir de l'objet de concept , cependant , elle est seulement appelé de generateConceptObject(jsonObjectList,definedConcept). </li>
					<li>D'abord pour être concordant avec la refactorisation du csv, on a fait que yml2JsonObject(string_content) accepte une string contenu au lieu d'un nom de fichier. On peut toujours lire le fichier à l'extérieur , le mettre dans une variable et appeler yml2JsonObject(string_content) sur cette variable.</li>
					<li>J'ai remarqué que si nous avions un contenu tel que {a:3,b:4, null, c:5 } , il était convertible en Json , mais la liste de concept restait vide parce que nous n'appelons pas generateConceptObject(jsonObjectList,definedConcept) qui est la seule fonction qui appelle generateConceptList(conceptObject) .  Alors pour un exemple d'un objet qui n'est pas dans une liste alors la liste de concept n'en tient pas compte ,ce qui est problématique.</li>
					<li>Pour remédier à la situation , nous avons créer un attribut accumulator qui est une array , qui après chaque appel de this.recursiveFetchAttribute(jsonObject,createConcept(th.conceptName,"concrete",[]),{}), ajoute la version de l'objet concept à cet appel là avant d'ajouter {concept : {}} qui toujours le dernier élément. </li>
					<li>Ensuite on prend cette liste, on l'inverse, de sorte à ce que le dernier élément soit le premier , l'avant-dernier le deuxième etc. et on prend this.accumulator.reverse()[1]. Parce que l'élément 1 <b>appelé élément objet-alpha</b>, est la dernière version de concept object</li>
					<li>On appelle finalement generateConceptList(conceptObject) avec comme paramètre l'objet-alpha et cela nous génère notre liste de concept en bonne et due forme.</li>
				</ul>
				<li>Vérifier que si null est une clé , après les changements que nous avions fait précédemment , nous devrions avoir en retour un attribut :  {"name" :"null","target":{"name" : "string"},"required":false} , test : {a:3,b:4, null, c:5 } devrait nous donner que listConcept.concepts[0].attribute[2] == {"name" :"null","target":{"name" : "string"},"required":false} </li>
				<li>Vérifier que si null est la valeur d'un attribut alors "a" : null donnerait l'attribut => {"name" :"a","target":{"name" : "string"},"required":false} </li>
				<li>Vérifier si une clé n'est pas null ou n'as pas un objet null , alors s'il a un objet non-null en tant que clé alors vérifier que dans le concept actuel , on ait un attribut <b>bêta</b> avec le nom de la clé</li>
				<li>Vérifier que l'attribut est de type "reference". </li>
				<li>Vérifier que le target a un accept.</li>
				<li>Vérifier que le nom de l'accept est le nom de la clé.</li>
				<li>Vérifier qu'il y a un concept qui porte le nom de la clé.</li>
				<li>Vérifier les clés seules , si la clé fait partie d'un ensemble, elle devrait redonner un attribut pourtant le nom de la clé</li>
				<li>cet attribut devrait être de type string </li>
				<li>Il ne devrait pas avoir d'accept</li>
				<li>le "required" de cet attribut devrait être true.</li>
			</li>
			<li>Ensuite nous vérifions la fonction generateConceptList(conceptObject) en lui donnant comme paramètre : 
				<li>Un objet vide</li>
				<li>Un objet avec juste 1 seule concept vide dedans {concept : {}}</li>
				<li>Un objet avec un seul concept et un seul attribut {concept : {attributeName : {} . </li>
				<li>Un objet "typique" avec plusieurs concepts et plusieurs attributs de toutes sortes.</li>
				<li></li>
			</li>
			<li> Une fois que generateConceptList(conceptObject) et les fonctions mentionnées précédemment passent les tests donnés , nous avons assez d'éléments pour conclure que l'algoritme de parsing de yml fonctionne ou tout au moins rempli ses besoins fonctionnels.</li>
		</ul>
	</li>
	<li>Ensuite , testons le parsing du xml : 
		<ul>
			<li>D'abord , tout comme le csv , le yml , nous allons faire le refactoring du xml.
				<ul>
					<li>Nous changeons tous les "new Attributes" pour des Object.create(Attribute).init(...,Object.create(Target).init(...),...)</li>
					<li>Nous changeons tous les "new Concept" pour des  Object.create(Concept).init(...)</li>
					<li>Nous enlevons les appels à jsdom et nous appelons directement l'objet DomParser(). </li>
					<li>Nous avons transformé nos appels de classes en des appels d'objets (dictionnaire).</li>
					<li>Nous avons ajouté des try catch à readXMLFile(filename) et parseXML2Document(xmlString) afin que ce soit plus testable.</li>
				</ul>
			</li>
			<li>D'abord on teste la fonction de lecture . <li>1) On rentre un fichier valide et normalement nous devrions avoir une string.</li>
			<li> 2) On rentre un fichier invalide et on teste et normalement cela devrait nous redonner un message d'erreur.</li>
			<li>3)Et on teste un fichier avec les bannière "?xml" et on vois si elles sont enlevées. Et finalement on insère null comme paramètre et cela devrait donner une erreur</li>
			<li> Ensuite , on teste la fonction parseXML2Document(xmlString). Il faut valider avec le paramètre null, cela devrait nous donner une erreur. Tandis que si nous rentrons une string xml valide , cela devrait nous donner un objet document. </li>
			<li>parseTree(targetNode): 
				<ul>
					<li>Vérifier avec  targetNode = noeud sans enfant , cela devrait nous redonner un concept avec le nom du noeud.</li>
					<li>Vérifier que ce concept ait une liste d'attributs vide.</li>
					<li>Vérifier avec targetNode.childNode = 1 enfant devrait redonner un concept avec le nom du concept et </li>
					<li>Vérifier qu'il a un seul attribut string.</li>
					<li>Vérifier avec targetNode ayant un attribut(le noeud a un attribut) , le concept devra avoir un attribut avec le nom de l'attribut A</li>
					<li>Vérifier que l'attribut A devra être une string.</li>
					<li>Vérifier avec targetNode ayant plus d'un attribut(le noeud a des attributs) , le concept devra avoir un attribut avec le nom de l'attribut A,B,C, etc. </li>
					<li>Vérifier que La liste d'attributs(concept) devrait être aussi grande que la liste d'attributs(noeud).</li>
					<li>On teste la fonction processChildNode(childNode,attributeSet,targetConcept) avec un custom childNode, custom attributeSet, custom targetConcept.</li>
					<li>Pour la fonction processChildNode(childNode,attributeSet,targetConcept) , on a trois cas : si le nom du noeud n'est pas là , si le nom de node est là juste une fois , ou si le nom du noeud est là plus d'une fois. On fait 3 test pour valider ce qui se passera </li>
					<li>...</li>
				</ul>
			</li>
		</ul>
	</li>
</ul>


- Note to self : 
I think i finally understood how to have the best of both world
the one that is function-object and testable
but also the one i'm used to in case i wanna add things how i want to
having two versions of the code
one that is testable in source , and the one were i have the comfy(with the keywords class and new ) code in ./internal 
so i can call node and see if it runs and how it runs without having to go back and forth.
- Rapport technique : 
introduction : 
- problème,  : nature de projet , qu'est-ce qu'on essaie de résoudre , pourquoi on fait tout ce qu'on fait 
- Notre plan : L'objectif visé par notre projet ,ce qui va valider notre solution - si ces points sont là , on a réussis
=========================================================================================================================================================
- Analyse des besoins , du problème , du requis pour que ce comportement soit présent 
- Architecture dont j'ai fait le schéma -> début juin 
- On rentre dans les détails de cette architecture : Comment chaque morceau de cette architecture rentre dans l'implémentation 
- En écrivant l'implémentation , on dit les limites de notre implémentations, les points faibles , ceux à améliorer , analyse de l'implémentation 
- On décrit les tests 
=========================================================================================================================================================
Conclusion : 
- On revient sur nos objectifs 
- À quel degré chaque objectif a été atteint 
- Ouverture : On a fait ça mais que la prochaine étape serait d'enrichir l'import et/ou d'ajouter l'export. 

Rapport Rose : oui 

