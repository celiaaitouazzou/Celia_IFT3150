## Semaine 8 : import 

### Lundi 20 juin : Codage Semaine 3 (YML)

<ul>
	<li>J'ai réorganisé les fichiers du répertoire : les fichiers inputs pour les tests dans tests/tests-input , les fichiers que je génère tests/tests-manual , les fichiers que je génère dynamiquement dans tests/tests-generated, cela facilitera les tests dynamiques quand on en aura</li>
	<li>Avant j'ai essayé d'autres moyens pour écrire le fichier avec appendFile : <a href="https://www.tutorialkart.com/nodejs/create-file-in-nodejs-using-node-fs-module/">https://www.tutorialkart.com/nodejs/create-file-in-nodejs-using-node-fs-module/</a></li>
	<li> J'ai une fonction d'écriture pour que les fichiers puisse être écrit dans tests/tests-generated avec : <a href="https://thewebdev.info/2022/03/06/how-to-overwrite-a-file-using-fs-in-node-js/">https://thewebdev.info/2022/03/06/how-to-overwrite-a-file-using-fs-in-node-js/</a></li>
	<li> J'ai cherché une librairie afin de convertir yml en json,j'ai consulté plusieurs ressources : 
		<ul>
			<li><a href="https://stackoverflow.com/questions/36973736/convert-yaml-to-json-using-javascript">https://stackoverflow.com/questions/36973736/convert-yaml-to-json-using-javascript</a></li>
			<li><a href="https://stackoverflow.com/questions/38781929/how-to-convert-json-to-yaml-in-javascript">https://stackoverflow.com/questions/38781929/how-to-convert-json-to-yaml-in-javascript</a></li>
			<li></li>
			<li>Puis finalement utiliser : <a href="https://www.npmjs.com/package/js-yaml">https://www.npmjs.com/package/js-yaml</a></li>
		</ul>
	</li>
	<li>On fera le parsage yml en 3 temps pour les types primitifs: 
		<ul>
			<li>on parse en prenant pour compte que tous les concept sont concrets</li>
			<li> <b>Fonctionnalité de similarité : </b> dans un premier temps , on a une collection tel que : [{...},{...},{...}{...}.]prend un ensemble (le premier) coll[0] = {...} et par défaut c'est notre pivot (et notre premier concept ) . On va comparer le pivot avec tout les autres pour classer les éléments.</li>
			<li>On le compare à tous les autres, si A est le super-ensemble d'un autre élément , les deux sont similaires sinon A est différent de ce sous-ensemble et il s'agit d'un tout nouveau concept (raffinnage)</li>
			<li>Ensuite, nous allons tenter de voir des similarité plus subtiles , par exemple : si dans un concept , nous sommes pour la plupart similaire mais dans le concept A il y a l'attribut : "date of birth" et dans l'autre l'attribut :"year of birth" il est possible de faire un rapprochement entre les deux pour dire qu'ils sont similaires. L'aviser à l'utilisateur qu'il y a x % de similarité entre ces deux concepts. </li>
			<li>Dans un 3e temps , faire participer l'utilisateur pour lui demander lorsqu'on voit qu'un concept est similaire à un autre, veut-il qu'il soit le même et que les attributs en questions soient facultatifs? ou veut-il que ce soit deux concepts différents? </li>	
		</ul>
		<li>On fait la même chose pour les types plus complexes (concept dans concept ou set de concept (Array.isArray) dans concept etc.)<br>
		<b><a href ="https://stackoverflow.com/questions/38304401/javascript-check-if-dictionary">https://stackoverflow.com/questions/38304401/javascript-check-if-dictionary</a></b>
		</li>
	</li>
	<li>Créé la classe : YMLParserSerializer avec un constructeur qui prend une string filename</li>
	<li>yml2JsonObject() : méthode qui prend this.filename et ressort un objet </li>
	<li>getAttributeOfOneElementOfYMLList(ymlListElement) qui extrait les éléments de ma liste dans mon dictionnaire et les retourne </li>
	<li>getAttributesOfAllElementOfYMLList () , applique cela à tous les éléments de l'objet json principal, celui retourné par le ParserYML</li>
	<li>comparer les attributs qui est supposé appeler checkIfIncluded qui elle-même est une fonction qui compare deux listes , voir si elle contient les mêmes éléments même si dans un ordre différent</li>
	<li> Liens utilisé et encore possiblement utiles: 
		<ul>
			<li><a href="https://stackoverflow.com/questions/201183/how-to-determine-equality-for-two-javascript-objects"></a>https://stackoverflow.com/questions/201183/how-to-determine-equality-for-two-javascript-objects</li>
			<li><a href="https://github.com/angular/angular.js/blob/6c59e770084912d2345e7f83f983092a2d305ae3/src/Angular.js#L670">https://github.com/angular/angular.js/blob/6c59e770084912d2345e7f83f983092a2d305ae3/src/Angular.js#L670</a></li>
			<li><a href="https://github.com/angular/angular.js/blob/6c59e770084912d2345e7f83f983092a2d305ae3/src/Angular.js#L670">https://github.com/angular/angular.js/blob/6c59e770084912d2345e7f83f983092a2d305ae3/src/Angular.js#L670</a></li>
			<li><a href="https://flexiple.com/javascript-array-equality/">https://flexiple.com/javascript-array-equality/</a></li>
			<li><a href="https://www.w3schools.com/js/js_object_sets.asp">https://www.w3schools.com/js/js_object_sets.asp</a></li>
			<li><a href="https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array/includes">https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Array/includes</a></li>
			<li><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Indexed_collections">https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Indexed_collections</a></li>
			<li><a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set">https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set</a></li>
			<li><a href="https://stackoverflow.com/questions/8866652/determine-if-2-lists-have-the-same-elements-regardless-of-order">https://stackoverflow.com/questions/8866652/determine-if-2-lists-have-the-same-elements-regardless-of-order</a></li>
		</ul>
		<li>Ceci étant dit : je vais tout retravailler à partir du fait que j'ai le yml parsé en json object</li>
		<li>
			<ul> Plus de ressources utiles:
				<li><a href="https://stackoverflow.com/questions/8511281/check-if-a-value-is-an-object-in-javascript">https://stackoverflow.com/questions/8511281/check-if-a-value-is-an-object-in-javascript</a></li>
			</ul>
		</li>
	</li>
</ul>

### Jeudi 23 juin 2020 : Codage Semaine 3 (YML)

Voici le pipeline que je suis en train de créer en supposant que j'ai mon objet json: 
<ol>
	<li>J'ai ajouté la fonction : retrieveAttribute(i,objectElement) qui prend un élément d'un dictionnaire et retourne l'équivalent en attribut.</li>
	<li>retrieveAccept() pour que si on a des sous structures sous-jacente on puisse les récupérer </li>
	<li>createAttributeList(object) qui prend un object (dans notre cas un élément de la liste d'objet qu'est le json) et itère à travers les clefs  i qui appelle retrieveAttribute(clef,jsonObject[clef]) retourne une liste d'attributs d'UN SEUL concept</li> 
	<li>generateConceptList() : appelle createAttributeList(object) pour chacun des objets dans la liste d'objets de l'objet json , avec la liste d'attributs pour chaque objet et l'attribut conceptName , on crée un attribut concret et on l'ajoute à la liste d'attribut. <b>On a alors une première version de la structure qu'on recheche(voir semaine 7)</b></li>
	<li>sameAttribute(x,) compare deux attributs x et y à savoir s'il ont le même nom , et la même structure, alors ils représentent le même attribut (j'ai essayé ceci : <a href="https://stackoverflow.com/questions/1068834/object-comparison-in-javascript">https://stackoverflow.com/questions/1068834/object-comparison-in-javascript</a>) mais finalement ,cela ne marchait pas alors j'ai fini par simplement : return JSON.stringify(x) == JSON.stingify(y) ce qui me donne de meilleurs résultats avec moins de code</li>
</ol>
