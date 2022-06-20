## Semaine 6 : Import  

### Lundi 6 juin 2022 : Début du codage 


<ul>
	<li>Maintenant qu'on a bien compris les bases de gentleman (ce qui inclut les primitives , et les formats acceptés et des fichiers qui sont pris en entrés par l'éditeur pour créer et manipuler les modèles.</li>
  <li>J'ai commencé à coder la conversion de soir_sample dynamiquement,soit : 
	<ul>
		<li>readAFile qui est une fonction qui prend un nom de fichier en string et retourne</li>
		<li>J'ai d'abord essayé avec readFile() : function readAFile(file) qui n'as pas marché plus particulièrement j'avais de la difficulté avec les exemples que j'ai trouvé en ligne à savoir : 
			<ul>
				<li><a href="https://nodejs.dev/learn/reading-files-with-nodejs"></a>https://nodejs.dev/learn/reading-files-with-nodejs</li>
				<li><a href="https://nodejs.org/en/knowledge/file-system/how-to-read-files-in-nodejs/">https://nodejs.org/en/knowledge/file-system/how-to-read-files-in-nodejs/</a></li>
				<li><a href="https://www.geeksforgeeks.org/node-js-fs-readfile-method/">https://www.geeksforgeeks.org/node-js-fs-readfile-method/</a></li>
				<li><a href="https://stackabuse.com/read-files-with-node-js/">https://stackabuse.com/read-files-with-node-js/</a></li>
				<li><a href="https://www.w3schools.com/nodejs/nodejs_filesystem.asp">https://www.w3schools.com/nodejs/nodejs_filesystem.asp</a></li>
		</ul>
		<li>J'avais fait dans un premier temps la fonction readAFile(file) qui prend un nom de fichier et retourne en string (J'ai fait plusieurs itération de cette fonction plus spécifiquement l'erreur "no such file or directory" quand le fichier en question était dans le même répertoire que le fichier de code ou que le code n'arrivait pas à trouver mon fichier de fonction).</li>
		<li>parseCSV() qui cherche à savoir quel type de données est-ce que la column représente(int,bool,ou string) tel que présenté ici : <a href="https://github.com/geodes-sms/gentleman/commit/c0cdc6e6020e423dd9bb09dd903c8e1a8e8b52b5">https://github.com/geodes-sms/gentleman/commit/c0cdc6e6020e423dd9bb09dd903c8e1a8e8b52b5</a></li>
		<li>Par la suite j'ai rajouté file2DDataFrame() qui prend la string donné en output par readAFile(file) en input et redonne un tableau 2D correspondant au CSV</li><br>
		<li>generateDictionnary() qui tente de prendre cette dataframe colonne par colonne comme ceci : <a href="https://stackoverflow.com/questions/40008479/reading-a-2d-array-by-column">https://stackoverflow.com/questions/40008479/reading-a-2d-array-by-column</a>et retourner la structure sérialisé qui va par la suite produire le json (cette fonction va être modifiée voire supprimé au cours de la semaine prochaine étant donné que j'avais de la difficulté à générer le json en question) tel que montré ici : <a href="https://github.com/geodes-sms/gentleman/commit/a05b05af8c6cb5d3ffbbc3dcd1c0a11d9b6bb54b"></a></li>
		</li>
		<li>finalement la fonction readAFile(file) a fini par marché et elle est inspirée de : <a href="https://www.geeksforgeeks.org/node-js-fs-readfilesync-method/">https://www.geeksforgeeks.org/node-js-fs-readfilesync-method/</a></li>
	</ul>
</ul>

### Jeudi 9 juin 2022 : codage continue

<ul>
</li>
	<li>Me familiariser avec javascript : <a href="https://www.w3schools.com/js/js_function_parameters.asp"></a></li>
	<li>J'ai supprimé la fonction parseCSV() qui n'ajoutait pas grand-chose et l'a remplacé par typeInference() qui est plus proche de l'inférence de type et j'ai fait plusieurs recherches afin de trouver les regex qui pourront m'aider à connaitre le type exacte de string qu'il s'agit 
		<ul>
			<li> Si l'élément de la dataframe de la 2e rangée (dataframe[1]) ne contiens que des nombres ,c'est un nombre : <a href="https://stackoverflow.com/questions/9011524/regex-to-check-whether-a-string-contains-only-numbers"></a>https://stackoverflow.com/questions/9011524/regex-to-check-whether-a-string-contains-only-numbers</li>
			<li>Si l'élément de la dataframe de la 2e rangée (dataframe[1]) ne contiens que des lettres comme ceci,c'est une string : <br> 
				- <a href="https://stackoverflow-com.translate.goog/questions/12778083/regex-with-space-and-letters-only?_x_tr_sl=en&_x_tr_tl=fr&_x_tr_hl=fr&_x_tr_pto=sc">https://stackoverflow-com.translate.goog/questions/12778083/regex-with-space-and-letters-only?_x_tr_sl=en&_x_tr_tl=fr&_x_tr_hl=fr&_x_tr_pto=sc</a> <br>
				- <a href="https://stackoverflow.com/questions/12778083/regex-with-space-and-letters-only">https://stackoverflow.com/questions/12778083/regex-with-space-and-letters-only</a><br>
			Mais est-ce un url, un email , une date ou un type reconnaissable de données? Quelles sont les données que gentleman peut comprendre?</li>
			<li>Après avoir bien observé les fichiers que j'ai fait la semaine dernière, toutes les données sont des strings pour le moment. Je me suis entendu avec Louis-Édouard que toutes les données seraient des strings en tout temps mais que nous pourrions faire des suggestions de types de données à l'interface.</li>
		</ul>
	 </li>
	<li>mais je ne sais toujours pas comment faire pour convertir ma dataframe en structure json</li>
	<li>J'ai séparé la fonction qui lit le fichier dans un autre fichier afin de mieux compartimentaliser mes fonctions et que les autres modules à venir (yml,xml) arrivent à importer et utiliser la fonction de cette façon : <a href="https://stackoverflow.com/questions/5797852/in-node-js-how-do-i-include-functions-from-my-other-files">https://stackoverflow.com/questions/5797852/in-node-js-how-do-i-include-functions-from-my-other-files</a></li>
	<li>J'ai enlevé generateDictionnary, et j'exporte ma fonction readAfile plus élégamment.</li>
</li>
</ul>