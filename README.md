# MongoDB-NodeJS-EXPRESS


MONGODB

MongoDB est un système de gestion de bases de données.
IL ne s'agit pas d'un SQL mais de bases de données NoSQL orientées documents.


Chaque entrée d’une base MongoDB est appelée document. Un document n’est rien d’autre qu’un objet JSON contenant une série de clefs/valeurs.
Un document MongoDB est comparable à une entrée au sein d’une table SQL. Les documents sont rassemblés au sein de collections, qui sont donc les homologues des tables SQL. 
Le fait de structurer les documents en utilisant une syntaxe JSON les rend faciles à manipuler, tout se fera en JavaScript, nul besoin d’apprendre un langage comme le SQL pour
faire des requêtes, et l’accès aux propriétés des documents se fera en JavaScript “natif”, comme s’il s’agissait d’objets tout à fait normaux.
A l’inverse des tables SQL, aucune structure n’est imposée par MongoDB. Chaque document d’une collection peut différer d’un autre ! C’est au développeur de faire attention à garder une structure cohérente pour ne pas se perdre.

1/ Installer MongoDB et tester

Voir la documentation et suivre les étapes d'installation: https://doc.ubuntu-fr.org/mongodb

2/ MongoDB installé - Quelques opérations

a/Ouvrir le shell (la console) nous permettant de commander MongoDB
b/Afficher toutes les bases de données gérées par MongoDB: commande show dbs
c/Changer de baseou créer une base: commande use <nom-de-la-base>
d/Insérer des documents: 
exemple: db.personnages.insert( { name : “Gordon Freeman”, game : “Half-Life” } ) ;
Cette simple commande insérera le document { name: "Gordon Freeman", game: "HalfLife" } au sein de la collection personnages. Cette collection n’existe pas, mais sera créée automatiquement.
e/Faire des recherches:db.personnages.find()
Avec spécification des: db.personnages.find( { name : "Gordon Freeman" } ).





SE CONNECTER DEPUIS NODE.JS

1/ Installer le module NPM mongodb : npm install mongodb.

2/ Connexion à la base de données:
var MongoClient = require("mongodb").MongoClient ;
[[information]] | MongoClient est similaire au MongoClient que l’on peut trouver pour d’autres
langages comme PHP, Python, Ruby…
Une fois que c’est fait, une connexion peut être amorcée grâce à la méthode connect() :
MongoClient.connect("mongodb://localhost/tutoriel", function(error, db) {
if (error) return funcCallback(error) ;
console.log("Connecté à la base de données 'tutoriel'") ;
}) ;
connect() reçoit deux paramètres : une URI définissant l’adresse du serveur MongoDB ainsi que
la base de données à utiliser (il s’agit ici de la base tutoriel), et une fonction de callback (j’utilise
ici une fonction anonyme).
La fonction de callback recevra deux paramètres : error et db. Si error est défini, c’est qu’il s’est
passé quelque chose empêchant la connexion. db est un objet qui représente la base de données,
et qui va nous permettre de communiquer avec cette dernière.

OPERATION DEPUIS NODE.JS

1/ObjectID: l’identifiant d’un document, il est toujours contenu dans la propriété _id.
Lorsque l’on insère un nouveau document dans une collection, MongoDB lui définit automatiquement une propriété _id qui va contenir un objet ObjectID, lequel représente l’identifiant du
document.

{
name : "Adrian Shephard",
game : "Half-Life: Opposing Force"
}
MongoDB lui définit alors un identifiant :
{
_id : ObjectID("53dfe7bbfd06f94c156ee96e"),
name : "Adrian Shephard",
game : "Half-Life: Opposing Force"
}

2/Récupérer des documents d'une collection
Il suffit d’utiliser l’objet db pour effectuer une requête. On utilise la méthode find() et on demande de recevoir les résultats sous la forme d’un tableau, via la méthode toArray().

MongoClient.connect("mongodb://localhost/tutoriel", function(error, db) {
if (error) throw error ;
db.collection("personnages").find().toArray(function (error, results) {
if (error) throw error ;
results.forEach(function(i, obj) {
console.log(
17
5 Opérations depuis Node.js
"ID : " + obj._id.toString() + "\n" // 53dfe7bbfd06f94c156ee96e
"Nom : " + obj.name + "\n" // Adrian Shephard
"Jeu : " + obj.game // Half-Life: Opposing Force
) ;
}) ;
}) ;
}) ;

