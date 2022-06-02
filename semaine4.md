## Import-Export : Semaine 4

### Lundi 23 mai 

- ajouter semaine 1 et semaine 2 

- concept  =  nom + type + primitive ou concept défini nous-même + attributs (optionnel ou pas ) , 

- contrainte après lieu : 


primitive : string , number, boolean , set , reference 

d'ici jeudi : faire le point , on voit l'implémentation de ça 
- implémentation des primitives 
- premièrement tranformation en considérant uniquement les primitives : int, string, boolean
- 2e temps : structure complexe -> structure imbriquées , les références , set 

fin de semaine : concret derivative 

-> cette semaine on aura prototypé des transformations simples.

- inclure les fichiers exemples dans le répertoire (done)

### Vendredi 27 mai 

Rencontre avec M.Syriani. On a revu le plan afin de faire l'import , principalement l'architecture, on a également vu le méta-modèle qui me permettrait de faire l'import. On a revu le diagramme de classe de gentleman trouvé dans le document de gentleman. 

- Faire les json des fichiers exemples 

#### Problème 

J'ai également update mes semaines et documenté le projet en incluant le prototype, l'analyse des besoins 

J'ai pas compris quand on me demandait de faire les fichiers équivalents si c'était les fichier **pouvant** donner les gentlemans de structures de données bibliothèques.xml,courses.yml,et soir_sample.csv ou si c'était les fichiers que si on avait un gentleman avec ces données et qu'on téléchargeait le json à partir de gentleman , ce qui représente un autre fichier. 

Je ne comprenais pas certains aspect des jsons, comme le target dans attributes , où dois-je mettre les données raw dans le fichier? Il faut que je consulte Louis-Édouard afin de savoir exactement à quoi devrait ressembler les outputs de ces 3 fichiers. 

J'ai quand même commencé par le soir_sample.csv. J'ai fait un concept arbitraire appelé "rangées" et les rangées en questions étaient les attributs que j'ai mis tel que : 


{
    "type":"concept",
    "concept":[
        {
            "name" : "rangee",
            "nature":"concrete",
            "attributes":[
                {
                    "name":"id",
                    "id": ["001","002","003","004","005","006"],
                    "required":true
                },
                {
                    "name":"first_name",
                    "first_name":["Pruthvi","kasyap","Rajesh", "Preethi", "Trupthi","Archana"],
                    "required":true
                },
                {
                    "name":"last_name",
                    "last_name":["Reddy","Sastry","Khanna","Agarwal","Mohanty","Mishra"],
                    "required":true
                },
                {
                    "name":"phone_no",
                    "phone_no":["9848022337","9848022338","9848022339","9848022330","9848022336","9848022335"],
                    "required":true
                },
                {
                    "name":"location",
                    "location":["Hyderabad" ,    "Vishakapatnam ",    "Delhi" ,    "Pune ",   " Bhubaneshwar" ,"Chennai"],
                    "required":true
                }
            ]
        }
    ]
}