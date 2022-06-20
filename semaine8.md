## Semaine 8 : import 

### Lundi 20 juin : Codage Semaine 3 (YML)

<ul>
	<li>J'ai réorganisé les fichiers du répertoire : les fichiers inputs pour les tests dans tests/tests-input , les fichiers que je génère tests/tests-manual , les fichiers que je génère dynamiquement dans tests/tests-generated, cela facilitera les tests dynamiques quand on en aura</li>
	<li> J'ai une fonction d'écriture pour que les fichiers puisse être écrit dans tests/tests-generated avec : <a href="https://thewebdev.info/2022/03/06/how-to-overwrite-a-file-using-fs-in-node-js/">https://thewebdev.info/2022/03/06/how-to-overwrite-a-file-using-fs-in-node-js/</a></li>
	<li> J'ai cherché une librairie afin de convertir yml en json,j'ai consulté plusieurs ressources : 
		<ul>
			<li><a href="https://stackoverflow.com/questions/36973736/convert-yaml-to-json-using-javascript">https://stackoverflow.com/questions/36973736/convert-yaml-to-json-using-javascript</a></li>
			<li><a href=""></a></li>
		</ul>
	</li>
	<li>On fera le parsage yml en 3 temps : 
		<ul>
			<li>on parse en prenant pour compte que tous les concept sont concrets</li>
			<li> <b>Fonctionnalité de similarité : </b> dans un premier temps , on a une collection tel que : [{...},{...},{...}{...}.]prend un ensemble (le premier) coll[0] = {...} et par défaut c'est notre pivot (et notre premier concept ) . On va comparer le pivot avec tout les autres pour classer les éléments.</li>
			<li>On le compare à tous les autres, si A est le super-ensemble d'un autre élément , les deux sont similaires sinon A est différent de ce sous-ensemble et il s'agit d'un tout nouveau concept (raffinnage)</li>
			<li>Ensuite, nous allons tenter de voir des similarité plus subtiles , par exemple : si dans un concept , nous sommes pour la plupart similaire mais dans le concept A il y a l'attribut : "date of birth" et dans l'autre l'attribut :"year of birth" il est possible de faire un rapprochement entre les deux pour dire qu'ils sont similaires. L'aviser à l'utilisateur qu'il y a x % de similarité entre ces deux concepts. </li>
			<li>Dans un 3e temps , faire participer l'utilisateur pour lui demander lorsqu'on voit qu'un concept est similaire à un autre, veut-il qu'il soit le même et que les attributs en questions soient facultatifs? ou veut-il que ce soit deux concepts différents? </li>
			<li></li>
		</ul>
	<li>
</ul>

### Jeudi 23 juin 2020 : Codage Semaine 3 (YML)