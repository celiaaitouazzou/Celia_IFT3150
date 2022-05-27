## Import-Export : Semaine 2

### Lundi 9 mai

- Commencé à faire des recherches sur ce qui interesserait l'utilisateurs en terme d'import. 
- Quels types de fichiers on aimerait pouvoir convertir? 
- Quels types de fichiers sont les plus populaires? 
- Quelles sont les parties qu'on peut convertir et celles qu'on doit laisser et expliquer pourquoi on a pas pu les convertir. 

Pendant mes recherches j'ai trouvé : 

- https://www.computerhope.com/issues/ch001789.htm
- https://blog.filestack.com/thoughts-and-knowledge/document-file-extensions-list/
- https://www.converter365.com/blog/most-common-file-extensions-for-windows/


Ici , j'ai noté ceux que je pensais qui seraient les plus intéressants pour l'utilisateur. 
Après avoir discuté de quels et quels types seraient convertible où pas (On avait déjà défini YAML comme un type convertible), on est venu à la conclusion qu'il fallait pour qu'un fichier soit convertible , il fallait que la partie du fichier soit étiquettée c'est-à-dire que ça donnée a un 'label' , une étiquette. Par exemple : 

<p align="center">

Bibliothèque : BANq  
Auteur : Jean-Jacaques Rousseau  
Titre : Rêveries du promeneur solitaire  
Éditions : Folio Classiques     
Dates de parution : 2006  
</p>


On a alors conclu qu'on aller se concentrer sur 3 types de fichiers : YAML, XML , et CSV. Étant donné que j'avais encore des problèmes de clonage avec mon ordinateur, on a setup gentleman avec un ordinateur du DIRO. 

On a à partir de là installé les dépendances nécessaires au fonctionnement de gentlemant npm et node. Et j'ai vu pour la première fois comment on pouvait le run.

Et de là , Louis-Édouard m'a expliqué l'architecture général du code, m'a montré les fichiers des modèles trafic lights et to do list . Et en général , comment le code fonctionnait , ce qu'il appelait à partir d'index, comment l'exécuter. 

