## Lundi 30 mai 2022

Après une discussion , on a établi que , par rapport à mes questions de la semaine dernière : 

- Les jsons représente la **structure générale** , l'ajout des données viendra après 
- le target représente les contraintes de la donnée, est-ce un set, une string , un int ? quel est le defaut de la donnée? et quelles sont les contraintes sur la données (longueur,cardinalité, regex etc.)
- le nom du concept peut être arbitraire 
- pour le csv les rangées sont les attributs , pour le yml un dictionnaire = une liste d'attribut 

À partir de là , modifions les jsons-exemples afin qu'ils correspondent à la structure désirée 

*à demander* : il faut que le modèle donné soit buidable ainsi *demander* quel sont les critères pour qu'un fichier json reçu en input soit buildable?

## Jeudi 2 juin 2022

 <ul>
  <li>Fini le soir_sample-manuel.json (Done) ce qui inclut</li>
	<ul>
		<li>concept que nous allons utiliser pour tous les csv, le concept de : "rangee" </li>
		<li>les rangees en questions seront les attributs que j'ai bien défini et défini au moins leur type</li>
		<li>Et puis c'est tout!</li>
	</ul>
	<li> - Fini le courses-manuel.json (Done) ce qui implique </li>
	<ul>
		<li>si aucun concept ne ressort du yml , on appellera le concept : concrete_concept  </li>
		<li>On assume comme pour le csv pour l'instant qu'on a un seul concept par fichier</li>
		<li>les champs du yml sont les attributs du concept </li>
	</ul>
	<li>-Fini le bibliothèque-manuel.json (Done) ce qui comprend</li>
	<ul>
		<li>On commence par la couche la plus extérieure et on la met en temps que concept A </li>
		<li>Ensuite tous les enfants de A sont mis en tant que set (à moins qu'on ait une référence xml alors on le déclare comme référence) et on vérifie si eux ont des enfants, si oui -> ils sont aussi des concepts complexe , sinon , ils sont des primitives(string,integer,boolean) </li>
	</ul>
</ul> 




