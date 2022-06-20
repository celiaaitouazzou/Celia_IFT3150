## Semaine 7 : Import 

### Lundi 13 juin 2022

<ul>
	<li>Dans un premier temps , j'ai conceptualisé une architecture de structure classe me facilitant la conversion et je m'aide à faire des classes avec <a href="https://www.w3schools.com/js/js_object_methods.asp">https://www.w3schools.com/js/js_object_methods.asp</a></li>
	<li>On appelle la classeConceptList qui est la première classe qu'on appelle qui a comme attributs un type qui est un string et une liste de concept qui est une list. </li>
	<li>ConceptList a également la méthode add_concept(), on ajoute un objet Concept à la liste de concept.</li>
	<li>Une classe Concept a quant à lui 3 attributs : le 'name' qui est une string , la 'nature' qui est une string, et 'attributes' qui est une liste contenant des objets attributes </li>
	<li>Une classe Attributes qui a un 'name' (string), un objet Target , et un 'required'(boolean) , </li>
	<li>Une classe Target qui a 3 attribut : 'name' le nom du type de l'attribut (string , number, boolean ,set , reference),'isAccept' boolean qui dit qu'un accept est nécessaire (dans le cas d'un set ou d'une référence) ou pas , et l'ensemble accept en question</li>
</ul>
<ul>
	<li> Dans un deuxième temps , on a le pipeline suivant : 
		<ol>
			<li>On lit le fichier avec readAFile(filename) ce qui nous redonne la string S</li>
			<li>On utilise la string S en input à file2DDataframe(S) ce qui nous redonne le tableau 2D D.</li>
			<li>Je vérifie la validité du fichier avec validation(D) voir si le fichier a le même nombre de colonnes dans chaque rangées (comme convenu dans le spécifications). </li>
			<li>Si le fichier est valide on continue avec le parsing du fichier csv , sinon on demande à l'utilisateur de changer son fichier.</li>
			<li>Une fois la validation faite et si c'est valide , on appelle initialize étant donné que tous les csv ont pour premier concept : *collection_de_rangees* comme établi précédemment lorsque nous validions à quoi devait ressembler nos inputs . En d'autre terme , un 'set' du concept rangées :
			{"name":"collection_de_rangees","nature":"concrete","attributes":[{"name": "row_set,required":true,"target":{"name":"set","accept":{"name":"rangee"}}}]} 
        	</li>
        	<li>Une fois ce premier concept initialisé , on l'ajoute à la liste de concept</li>
        	<li>Il reste maintenant à définir le concept de Rangées.</li>
        	<li>On commence ceci par create_attribute(dataf) . Cette fonction itère à travers la rangée header du csv afin de retirer les attributs du concept rangées. Chaque élément retiré est le nom de l'attribut. On appelle également get_target qui retourne un objet target de type string et on met required = true. </li>
        	<li>Une fois notre attribut fais on l'ajoute à la liste d'attribut 'listOfAttributes qu'on retourne à la fin de la fonction.</li>
        	<li>addToConceptToList va appeler la fonction avec le dataframe qu'on a et ensuite créé un concept qui a pour nom: "rangee", nature : "concrete" et pour liste d'attribut , la liste qu'on a créé avec create_attribute(dataf) et on rajoute ce concept à la liste de concept.</li>
        	<li>Finalement, on met la suite de fonctions dans l'ordre désiré à savoir : 
        		[```main () {
					var df = this.file2DDataFrame(",");
					csvps.initialize(
					"collection_de_rangees",
					"concrete",
					[new Attribute("row_set",new Target("set",true,{"name":"rangee"}),true)]);
					if(this.validation(df)){
					csvps.addConceptToList(df);             
					} 
				}
				```]
    		</li>
		</ol> 
	</li>
</ul>

## Jeudi 16 juin 2022 

<ul>
	<li>Maintenant que nous avions la structure voulue, nous ne l'avions pas dans le format voulu. </li>
	<li>Nous avions par exemple: <br>
		<img src ="datastructurecsv1.png" alt="bad data structure"></img>
	</li>
	<li>Les éléments Objets contenait ce qu'ils devaient contenir mais ceci n'aidait pas à contruire la structure sous la forme json désiré</li>
	<li>Alors on a construit une pipeline qui permettrait de le faire à partir de la structure que nous avions établi: <br>
		<ol>
			<li>On crée un objet ListConcept listConcept</li>
			<li>listConcept.main() afin d'avoir notre structure remplie en bonne et due forme</li>
			<li>On appelle listConcept et on appelle listConcept.printConceptList(); </li>
			<li>printListConcept initialise la string qui accumule la structure (la string builder si vous voulez), et qui accumule {type : concept ,concept : [...et à ce moment on itère à travers la liste de concept et pour chacun de ces concepts on appelle concept[i].printConcept()...]  </li>
			<li>concept.printConcept() de son coté, accumule le nom du concept sa nature et itère à travers les attributs en appelant pour chacun des attribute[i].printAttribute()</li>
			<li>par la suite , attribute.printAttribute accumule le nom de l'attribut, le target par l'entremise de la fonction printTarget qui accumule target et le Accept en parcourant le dictionnaire récusivement avec un For in (<a href="https://www.w3schools.com/js/js_loop_forin.asp">https://www.w3schools.com/js/js_loop_forin.asp</a>)s'il y a lieu et retourne la string accumulé à printAttribute pour compléter et printAttribute complète avec 'required'</li>
			<li>Une fois l'attribute bien fait il retourne son résultat à printConcept qui l'ajoute à ce qu'il avait déjà pour faire un concept complet </li>
			<li>printConceptList l'ajoute au reste de la collection des concepts établis</li>
			<li>On a alors la structure voulue , il manque plus qu'à prendre cette structure et l'écrire dans un json et cela sera valide </li>
		</ol>
	</li>
</ul>

### Il reste à : 
<ul>
	<li>créer une fonction d'écriture une fois que tout le pipeline csv sera testé afin d'en faire des jsons</li>
	<li>Indiquer dans l'interface lorsque le fichier n'est pas convertible.</li>
	<li>Faire les suggestions de types une fois que l'import sera fini afin de rendre l'import plus user-friendly</li>
	<li>Faire plus de tests par rapport au jsons que cela donne voir si cela marche dans tous les cas valides (Autant de colonnes partout). </li>
	<li>ajuster à a fin des arrays pour pas avoir de virgules : <br> 
		<a href="https://stackoverflow.com/questions/3216013/get-the-last-item-in-an-array">https://stackoverflow.com/questions/3216013/get-the-last-item-in-an-array</a><br>
		<a href="https://stackoverflow.com/questions/26241478/reverse-lookup-object-with-array">https://stackoverflow.com/questions/26241478/reverse-lookup-object-with-array</a><br>
		<a href="https://stackoverflow.com/questions/26241478/reverse-lookup-object-with-array">https://stackoverflow.com/questions/26241478/reverse-lookup-object-with-array</a>
	</li>
	<li>Optimiser les fonctions de print afin qu'elle soit moins lourdes et plus maintenables.</li>
	<li>Ajouter les données (instacier les concepts) pour le csv après avoir fait les structures pour yml</li>
</ul>