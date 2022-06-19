## Semaine 7 : Import 

### Lundi 13 juin 2022

<ul>
	<li>Dans un premier temps , j'ai conceptualisé une architecture de structure me facilitant la conversion </li>
	<li>On appelle la classeConceptList qui est la première classe qu'on appelle qui a comme attributs un type qui est un string et une liste de concept qui est une list. </li>
	<li>ConceptList a également la méthode add_concept(), on ajoute un objet Concept à la liste de concept.</li>
	<li>Une classe Concept a quant à lui 3 attributs : le 'name' qui est une string , la 'nature' qui est une string, et 'attributes' qui est une liste contenant des objets attributes </li>
	<li>Une classe Attributes qui a un 'name' (string), un objet Target , et un 'required'(boolean) , </li>
	<li>Une classe Target qui a 3 attribut : 'name' le nom du type de l'attribut (string , number, boolean ,set , reference),'isAccept' boolean qui dit qu'un accept est nécessaire (dans le cas d'un set ou d'une référence) ou pas , et l'ensemble accept en question</li>
</ul>
