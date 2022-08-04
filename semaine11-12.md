## Semaine 9-10 : semaine du 18 juillet et semaine du 25 juillet

### Finir la conversion du xml

<ul>
	<li>D'abord , il fallait trouver un moyen d'utiliser l'objet </li>
	<li>J'ai d'abord essayé cette librairie : <a href="https://developer.mozilla.org/fr/docs/Web/API/DOMParser">https://developer.mozilla.org/fr/docs/Web/API/DOMParser</a>. Cela n'a pas marché , les fonctions de DOMParser ne marchait pas même lorsque Gentleman était ouvert et avec internet. </li>
	<li>J'ai ensuite essayé la librairie dom-parser de npm : <a href="https://www.npmjs.com/package/dom-parser">. Elle non plus ne marche pas , elle me donne {dom : htmlParser: '<...>' }} mais on pouvait pas extraire un enfant en particulier puisque tout était en string. À ce point , autant moi-même parser la string , alors j'ai abandonné cette option.</li>
	<li>J'ai également essayé la librairie xmldom : <a href="https://github.com/xmldom/xmldom">https://github.com/xmldom/xmldom</a> et sans surprise, ce ne convenait pas . Cela me donnait effectivement un objet , mais il était vide ainsi , je ne pouvais extraire ses enfants ni sa racine et les méthode tel que document.getElementById(...) ne marchaient pas plus. Alors j'ai tenté autre chose. </li>
	<li>
	<li></li>


	
<li><a href="https://www.w3schools.com/jsref/prop_node_firstchild.asp">https://www.w3schools.com/jsref/prop_node_firstchild.asp</a> </li>
<li><a href="https://www.w3schools.com/xml/dom_nodes_access.asp">https://www.w3schools.com/xml/dom_nodes_access.asp</a></li>
<li><a href="https://developer.mozilla.org/en-US/docs/Web/API/Document">https://developer.mozilla.org/en-US/docs/Web/API/Document</a></li>
<li><a href="https://www.w3schools.com/xml/dom_nodes_access.asp">https://www.w3schools.com/xml/dom_nodes_access.asp</a></li>
<li><a href="https://www.javascripttutorial.net/javascript-dom/javascript-get-child-element/">https://www.javascripttutorial.net/javascript-dom/javascript-get-child-element/</a></li>
<li><a href="https://attacomsian.com/blog/javascript-dom-check-if-an-element-has-children">https://attacomsian.com/blog/javascript-dom-check-if-an-element-has-children</a></li>
<li><a href="https://developer.mozilla.org/fr/docs/Web/API/Document/documentElement">https://developer.mozilla.org/fr/docs/Web/API/Document/documentElement</a> </li>
<li><a href="https://www.javascripttutorial.net/javascript-dom/javascript-get-child-element/">https://www.javascripttutorial.net/javascript-dom/javascript-get-child-element/</a></li>
<li><a href="https://attacomsian.com/blog/javascript-dom-check-if-an-element-has-children">https://attacomsian.com/blog/javascript-dom-check-if-an-element-has-children</a></li>
<li><a href="https://developer.mozilla.org/fr/docs/Web/API/Element/hasAttribute">https://developer.mozilla.org/fr/docs/Web/API/Element/hasAttribute</a> </li>
<li><a href="https://developer.mozilla.org/fr/docs/Web/API/Element/attributes">https://developer.mozilla.org/fr/docs/Web/API/Element/attributes</a></li>
<li><a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element#svg_and_mathml">https://developer.mozilla.org/en-US/docs/Web/HTML/Element#svg_and_mathml</a></li>
<li><a href = "https://attacomsian.com/blog/javascript-dom-get-the-parent-of-an-element">https://attacomsian.com/blog/javascript-dom-get-the-parent-of-an-element</a></li>
<li><a href = "https://www.w3schools.com/jsref/prop_element_childelementcount.asp">https://www.w3schools.com/jsref/prop_element_childelementcount.asp</a></li>
<li><a href = "https://www.freecodecamp.org/news/check-if-javascript-array-is-empty-or-not-with-length/">https://www.w3schools.com/jsref/prop_element_childelementcount.asp</a></li>
</ul>