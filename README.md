# nodeJs-mongodb-blog
un petite projet basé sur nodeJs et mongoDB 


## installation des pre-requis et lancer le blog

pour executer ce projet, dabord il faux avoir la liste des outils suivant:

1. Base de données MongoDb
2. NodeJs serveur
3. Yarn pour installer les package du project
4. ExpressJs comme une language côte serveur
5. Ejs pour organiser, générer, et créer des template html
6. Bootsptrap pour un mieux design


### Base de données Mongodb

1.  [télécharger MongoDb et MongodbCompass](https://www.mongodb.com/download-center/community) (il faut choisir votre Systéme d'expoloitation). cliquer sur serveur tab pour la base de données et sur outils -> compass pour telecharger l'interface graphique du base de données.
2. installer MongoDb et compass vous trouverai un tutorial [ici](https://medium.com/@LondonAppBrewery/how-to-download-install-mongodb-on-windows-4ee4b3493514)
3. ajouter mongo à les variables d'environment. suivi le tutorial [ici](https://dangphongvanthanh.wordpress.com/2017/06/12/add-mongos-bin-folder-to-the-path-environment-variable/)

### NodeJS

1. télecharger NodeJS LTS [ici](https://nodejs.org/en/download/) 
2. installer

### Yarn 

1. télécharger Yarn [ici](https://yarnpkg.com/lang/en/docs/install/#windows-stable)
2. installer


## ExpressJs et Ejs et Bootstrap

ces outils sont déja inclus sur le dossier du projet. il faut juste cliquer SHIFT + clique droite dans la souris dans le dossier du projet.

choisir ouvrir une fenetre de commande ici

executer la commande suivant, pour installer les package du projet

    npm install

puis la commande , pour demarer la base de données

    mongod
    
 puis la commande , pour lancer le projet 

    node app.js 

le projet sera disponible sur le lien :  [http://localhost:3000/](http://localhost:3000/)




## explication de la structure et code de projet

### structure du project
notre projet se divise a trois partie:

1. le ficher app.js qui gére le site, ca veut dire, il contient le code de connextion à la base de données et la generation des page html des article du blog, le traitement du formulaire de l'ajoute du blog ... etc
2. le dossier Views qui contient les fichier html.
3. le dossier static qui contient les image et les fichier de style css.

### structure des pages html

chaque page contient :

1. la partie head contient importation des fichiers de style css et les fichiers de style bootstrap
2. le menu de navigation
3. le header (une grande image avec le titre du page au milieu)
4. le contenu du page 
5. la partie footer contient l'imporation des fichier de javascript du notre site et du bootstrap

pour la reduction du code et organisé/optimiser notre projet 
on a inclus le code html head dans un fichier head.ejs

le code html du menu de navigation dans navigation.ejs

le code de footer dans footer.ejs

et dans chaque page on inclus ces partie chacun avec une seul ligne avec la commande de ejs

     <%- include("partials/navigation") %>

comme ça si on modifie le code de chaqun de ces composants il va être modifier dans toutes les pages html.

alors nos fichers html va être écrit de avec la structure suivant

    <html>
    <head>
    <%- include("partials/head") %>
    </head>
    <body>
    <header class="header">
      <%- include("partials/navigation") %>
    </header>

    <!-- le contenu du page -->

    <%- include("partials/footer") %>
    </body>
    </html>
    
### example de fonctionnemnt du server

on a dit que app.js gére le connexion et les traitement des données entre le base de données et les ficher html

et ça de la maniére suivant:

lorsqu'on veut visiter la page animaux par example qui contient le catalogue des article des animaux dans notre blog.

on visite le lien http://localhost/animaux

à ce moment le serveur excute la fonction liée a ce page dans le fichier app.js

    app.get("/animaux", (req, res) => {
    Article.find({}, (err, article) => {
    res.render("animaux", { animaux: article });
    });
    });
cet fonction lance une requete pour recuperer toutes les acticle des animaux dans la base de données. et puis le serveur envoi le page html des animaux avec les articles qui sont dans la base données.

et dans le fichier html animaux.html on recupere les articles dans le variable animaux 
et on genere un table html des articles des animaux chaqun dans une cellule de table comme un lien vers la page de cette article avec une image de l'article, autrement dit 
si on a 3 article on aura 3 cellule (<td>), si ona 10 article dans la base donnees on aura 10 cellule
      
      <table>
          <tr>
            <% for(let i = 0; i < animaux.length; i++) { %>
            <td>
              <a href="/article?id=<%= animaux[i]._id.toString() %>">
                <img
                  src="../img/<%= animaux[i].catalogue %>"
                  width="300"
                  height="400"
                /><br />
                <center>
                  <font size="5"> <%= animaux[i].titre %></font>
                </center></a
              >
            </td>
            <% if((i-1)%3 === 0 && (i+1)!==animaux.length ){ %> </tr><%} %>
            <% } %>
            
          </tr>
        </table>
      
le resultat et un site web dynamique, pour ajouter une nouvelle page d'article il suffit d'ajouter une nouvelle entrée dans la base de données ou remplir la formulair qui va faire la meme chose atravers le fichier app.js



