## Semaine 9-10 : semaine du 18 juillet et semaine du 25 juillet

### Finir la conversion du xml

<ul>
	<li>D'abord , il fallait trouver un moyen d'utiliser l'objet </li>
	<li>J'ai d'abord essayé cette librairie : <a href="https://developer.mozilla.org/fr/docs/Web/API/DOMParser">https://developer.mozilla.org/fr/docs/Web/API/DOMParser</a>. Cela n'a pas marché , les fonctions de DOMParser ne marchait pas même lorsque Gentleman était ouvert et avec internet. </li>
	<li>J'ai ensuite essayé la librairie dom-parser de npm : <a href="https://www.npmjs.com/package/dom-parser">. Elle non plus ne marche pas , elle me donne {dom : htmlParser: '<...>' }} mais on pouvait pas extraire un enfant en particulier puisque tout était en string. À ce point , autant moi-même parser la string , alors j'ai abandonné cette option.</li>
	<li>J'ai également essayé la librairie xmldom : <a href="https://github.com/xmldom/xmldom">https://github.com/xmldom/xmldom</a> et sans surprise, ce ne convenait pas . Cela me donnait effectivement un objet , mais il était vide ainsi , je ne pouvais extraire ses enfants ni sa racine et les méthode tel que document.getElementById(...) ne marchaient pas plus. Alors j'ai tenté autre chose. </li>
	<li>
	<li>1.Finalement, on a décidé d'aller avec la librairie JSDOM : <a href ="https://github.com/jsdom/jsdom">https://github.com/jsdom/jsdom</a>, qui permet de retourner un object document et ainsi d'utiliser les fonctions de XMLDom(). Donc on commence par lire le fichier qui nous retourne une string s . Puis on prend cette string s et on enlève les entêtes du document qui ont '< ?xml ... ' ce qui donne une string s'. Puis on prend s' et on la convertit en un objet document qu'on retourne.</li>
	<li>2. La fonction parseTree(targetNode) , prend un élément et navigue à travers toute sa descendance et pour chaque noeud de sa descendance traite le noeud ce qui implique : 
		<ul>
			<li>2.1. On appelle targetNode.childNodes ce qui retourne la liste du noeud courant : <a href="https://www.javascripttutorial.net/javascript-dom/javascript-get-child-element/">https://www.javascripttutorial.net/javascript-dom/javascript-get-child-element/</a>.</li>
			<li>Chaque appel de la fonction représente un concept. On crée un objet qui contient les attributs de ce concept de manière unique . Et on crée aussi un nouveau concept. </li>
			<li>D'abord, on appelle qui prend en paramètre un noeud de l'objet Document. Cette fonction prend le noeud et s'il a des attributs, itère à travers les attributs et génère un objet string à partir du nom de l'attribut et les accumule (les objets attributs) dans une liste qu'on retourne. Par la suite la liste d'attribut du concept concatène la liste retournée par getNodeAttribute(cibleNode)</li>
		</ul>
	</li>



<li><a href="https://www.w3schools.com/jsref/prop_node_firstchild.asp">https://www.w3schools.com/jsref/prop_node_firstchild.asp</a> </li>
<li><a href="https://www.w3schools.com/xml/dom_nodes_access.asp">https://www.w3schools.com/xml/dom_nodes_access.asp</a></li>
<li><a href="https://developer.mozilla.org/en-US/docs/Web/API/Document">https://developer.mozilla.org/en-US/docs/Web/API/Document</a></li>
<li></li>
<li><a href="https://attacomsian.com/blog/javascript-dom-check-if-an-element-has-children">https://attacomsian.com/blog/javascript-dom-check-if-an-element-has-children</a></li>
<li><a href="https://developer.mozilla.org/fr/docs/Web/API/Document/documentElement">https://developer.mozilla.org/fr/docs/Web/API/Document/documentElement</a> </li>
<li><a href="https://developer.mozilla.org/fr/docs/Web/API/Element/hasAttribute">https://developer.mozilla.org/fr/docs/Web/API/Element/hasAttribute</a> </li>
<li><a href="https://developer.mozilla.org/fr/docs/Web/API/Element/attributes">https://developer.mozilla.org/fr/docs/Web/API/Element/attributes</a></li>
<li><a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element#svg_and_mathml">https://developer.mozilla.org/en-US/docs/Web/HTML/Element#svg_and_mathml</a></li>
<li><a href = "https://attacomsian.com/blog/javascript-dom-get-the-parent-of-an-element">https://attacomsian.com/blog/javascript-dom-get-the-parent-of-an-element</a></li>
<li><a href = "https://www.w3schools.com/jsref/prop_element_childelementcount.asp">https://www.w3schools.com/jsref/prop_element_childelementcount.asp</a></li>
<li><a href = "https://www.freecodecamp.org/news/check-if-javascript-array-is-empty-or-not-with-length/">https://www.freecodecamp.org/news/check-if-javascript-array-is-empty-or-not-with-length/</a></li>
</ul>