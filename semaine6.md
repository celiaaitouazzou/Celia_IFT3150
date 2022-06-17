## Semaine 6 : Import  

### Lundi : Début du codage 

- Ce qui incluait : 

<ul>
  <li>J'ai commencé à coder la conversion de soir_sample dynamiquement : 
	<ul>
		<li>readAFile qui est une fonction qui prend un nom de fichier en string et retourne</li>
		<li>J'ai d'abord essayé avec readFile() : <br>
			<p>
				function readAFile(file){<br>
var fs = require('fs');<br>
var data ="";<br>
try {<br>
    data = fs.readFileSync(file, 'utf8');<br>
    return data;<br>
} catch(e) {<br>
    console.log('Error:', e.stack);<br>
}<br>

}<br>
			</p>
			
</li>
		<li>Milk</li>
	</ul>
  </li>
  <li>on a compris les bases de gentleman (ce qui inclut les primitives , et les formats acceptés et des fichiers qui sont pris en entrés par l'éditeur pour créer et manipuler les modèles.</li>
  <li>Milk</li>
</ul>