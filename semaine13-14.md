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
					<li>cette fonction accepte 3 type d'élément : une array , un objet , une paire (clé valeur)</li>
					<li>On va tester si on a null, tel qu'on a un objet {a:3,b:4, null, c:5 }, je ne sais pas ce que nous ferions parce que ce cas n'est pas prévu dans le code. <b> À faire : Nous verrons comment implémenter cette logique dans le code. </b> </li>
					<li>si null est une clé , cela est couvert par contre.</li>
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
===========================================================================================================================================================
- Analyse des besoins , du problème , du requis pour que ce comportement soit présent 
- Architecture dont j'ai fait le schéma -> début juin 
- On rentre dans les détails de cette architecture : Comment chaque morceau de cette architecture rentre dans l'implémentation 
- En écrivant l'implémentation , on dit les limites de notre implémentations, les points faibles , ceux à améliorer , analyse de l'implémentation 
- On décrit les tests 
==========================================================================================================================================================
Conclusion : 
- On revient sur nos objectifs 
- À quel degré chaque objectif a été atteint 
- Ouverture : On a fait ça mais que la prochaine étape serait d'enrichir l'import et/ou d'ajouter l'export. 

Rapport Rose : oui 

