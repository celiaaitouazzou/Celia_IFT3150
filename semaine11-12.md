## Semaine 9-10 : semaine du 18 juillet et semaine du 25 juillet

### Finir la conversion du xml

<ul>
	<li>D'abord , il fallait trouver un moyen d'utiliser l'objet </li>
	<li>J'ai d'abord essayé cette librairie : <a href="https://developer.mozilla.org/fr/docs/Web/API/DOMParser">https://developer.mozilla.org/fr/docs/Web/API/DOMParser</a>. Cela n'a pas marché , les fonctions de DOMParser ne marchait pas même lorsque Gentleman était ouvert et avec internet. </li>
	<li>J'ai ensuite essayé la librairie dom-parser de npm : <a href="https://www.npmjs.com/package/dom-parser">. Elle non plus ne marche pas , elle me donne {dom : htmlParser: '<...>' }} mais on pouvait pas extraire un enfant en particulier puisque tout était en string. À ce point , autant moi-même parser la string , alors j'ai abandonné cette option.</li>
	<li>J'ai également essayé la librairie xmldom : <a href="https://github.com/xmldom/xmldom">https://github.com/xmldom/xmldom</a> et sans surprise, ce ne convenait pas . Cela me donnait effectivement un objet , mais il était vide ainsi , je ne pouvais extraire ses enfants ni sa racine et les méthode tel que document.getElementById(...) ne marchaient pas plus. Alors j'ai tenté autre chose. </li>
	<li>
	<li>1.Finalement, on a décidé d'aller avec la librairie JSDOM : <a href ="https://github.com/jsdom/jsdom">https://github.com/jsdom/jsdom</a>, qui permet de retourner un object document et ainsi d'utiliser les fonctions de XMLDom(). Donc on commence par lire le fichier qui nous retourne une string s . Puis on prend cette string s et on enlève les entêtes du document qui ont '< ?xml ... ' ce qui donne une string s'. Puis on prend s' et on la convertit en un objet document qu'on retourne.</li>
	<li>
		<ul>
			Ressources utilisées pour cette étape : 
			<li><a href="https://developer.mozilla.org/en-US/docs/Web/API/Document">https://developer.mozilla.org/en-US/docs/Web/API/Document</a></li>
		</ul>
	</li>
	<li>2. La fonction parseTree(targetNode) , prend un élément et navigue à travers toute sa descendance et pour chaque noeud de sa descendance traite le noeud ce qui implique : 
		<ul>
			<li>2.1. On appelle targetNode.childNodes ce qui retourne la liste du noeud courant : <a href="https://www.javascripttutorial.net/javascript-dom/javascript-get-child-element/">https://www.javascripttutorial.net/javascript-dom/javascript-get-child-element/</a>.</li>
			<li>Chaque appel de la fonction représente un concept. On crée un objet qui contient les attributs de ce concept de manière unique . Et on crée aussi un nouveau concept. </li>
			<li>D'abord, on appelle qui prend en paramètre un noeud de l'objet Document. Cette fonction prend le noeud et s'il a des attributs, itère à travers les attributs et génère un objet string à partir du nom de l'attribut et les accumule (les objets attributs) dans une liste qu'on retourne. Par la suite la liste d'attribut du concept concatène la liste retournée par getNodeAttribute(cibleNode)
				<ul>Ressources utilisées : 
					<li><a href="https://developer.mozilla.org/fr/docs/Web/API/Element/hasAttribute">https://developer.mozilla.org/fr/docs/Web/API/Element/hasAttribute</a> </li>
					<li><a href="https://developer.mozilla.org/fr/docs/Web/API/Element/attributes">https://developer.mozilla.org/fr/docs/Web/API/Element/attributes</a></li>
				</ul>
			</li>
			<li>On itère à travers les enfants de targetNode et pour chaque enfant : 
				<ul>
					<li>On appelle processChildNode(childNode,attributeSet,targetConcept) qui prend un noeud , un attributeSet qui est un ensemble d'attribut clé , valeur où la clé est le nom de du nom et la clé est le nombre de fois que le nom de l'enfant est apparu pour ce concept. Si on voit ce nom pour la première fois , on l'ajoute à attribute set et lui mettre une occurrence de 1. Sinon on incrémente la valeur de la clé . Si on a un enfant qui apparait plus d'une fois , on l'ajoute dans la liste d'attribut comme étant un 'set' et  dans attributeSet[nom] = -1 et on ne modifie plus la valeur de la clé dans attribute set.Donc de cette facon , on a juste une fois chaque attribute set.</li>
					<li>Ensuite on prend tous les enfants qui apparaissent juste une fois, et on les ajoute à la liste de concept comme des attributes "string"</li>
					<li>Si la liste d'attributs à la fin des deux étapes précédentes n'est pas vide ,alors on ajoute le concept à la liste de concept.</li>
					<li>Si l'enfant a des enfants, on fait un appelle récurisive qui fait que nous revenons à l'étape 2. où targetNode est le childNode en question.</li>
					<li>
						<ul>Ressources utilisées: 
							<li><a href = "https://www.freecodecamp.org/news/check-if-javascript-array-is-empty-or-not-with-length/">https://www.freecodecamp.org/news/check-if-javascript-array-is-empty-or-not-with-length/</a></li>
							<li><a href="https://attacomsian.com/blog/javascript-dom-check-if-an-element-has-children">https://attacomsian.com/blog/javascript-dom-check-if-an-element-has-children</a></li>
						</ul>
					<li>
					</ul>
				</ul>
			</li>
			<li>Et bien sûr on appelle parseTree en lui donnant comme paramètre de départ la racine et on a trouvé comment faire via la documentation js :<a href="https://developer.mozilla.org/fr/docs/Web/API/Document/documentElement">https://developer.mozilla.org/fr/docs/Web/API/Document/documentElement</a> .</li>
			<li>3.On appelle ensuite deleteSameConcept() qui ne prend rien en attribut étant donné qu'elle travaille entièrement sur la liste de concept qui est un attribut de la classe XMLParserSerializer, la classe sur laquelle nous somme en train de travailler. Pour chaque i dans la liste de concept et chaque j dans la liste de concept , on appelle nettoyerListElement(i,j,listOfConcept) (listOfConcept , qui est juste notre liste de concept) afin de nettoyer la liste de concept </li>
			<li> 3.1nettoyerListElement(i,j,listOfConcept) : si i != j , on a affaire à deux objets différents. Donc j'ai d'abord essayé de supprimer dynamiquement le concept, mais cela ne marchait pas parce que cela affectait l'itération des éléments et cela marchait à moitié. Alors, ce que j'ai opté plutôt que cette méthode c'est mettre l'élément à supprimer comme étant null. </li>
			<li>Voici comment cela fonctionne : 
				<ul>
					<li>Si deux objets concepts sont complètement identique , on met que le concept i est null </li>
					<li>S'ils ne sont pas identique , mais un concept a le même nom que l'autre objet concept , mais il a plus d'attributs que l'autre, on le garde lui et on met l'autre comme étant null.</li>
					<li>Si les deux concepts ne sont pas identique , ils ont le même nom et ont le même nombre d'attributs , alors on garde celui tel que JSON.Stringify(concept1).length > JSON.Stringify(concept2).length. En gros, on garde le concept qui en string est plus long que l'autre.</li>
				</ul>
			</li>
			<li>3.2. Une fois qu'on a notre listOfConcept avec les nulls à certain éléments. On appelle filter pour ne retenir que les éléments qui ne sont pas null ce qui conclut notre nettoyage <b> et ce qui conclut le parsing xml.</b></li>
		</ul>
		<li>Autres ressources consultées afin de faire le parsing : 
			<ul>
				<li><a href="https://www.w3schools.com/jsref/prop_node_firstchild.asp">https://www.w3schools.com/jsref/prop_node_firstchild.asp</a> </li>
				<li><a href="https://www.w3schools.com/xml/dom_nodes_access.asp">https://www.w3schools.com/xml/dom_nodes_access.asp</a></li>
				<li><a href = "https://attacomsian.com/blog/javascript-dom-get-the-parent-of-an-element">https://attacomsian.com/blog/javascript-dom-get-the-parent-of-an-element</a></li>
				<li><a href = "https://www.w3schools.com/jsref/prop_element_childelementcount.asp">https://www.w3schools.com/jsref/prop_element_childelementcount.asp</a></li>
			</ul>
		</li>
	</li>



