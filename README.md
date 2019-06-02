# Projet Génie Logiciel - Groupe 4C

Partie 3 (web) du sujet 4 : **Réservation de ressources étudiant**

Auteurs : Éléa Thuilier, Thomas Choquard, Sacha Wanono, Ulysse Guyon

[![Logo PolyLend](./public/image/logo-readme.png "Lien vers le serveur distant de PolyLend")](http://hyblab.polytech.univ-nantes.fr/4C/)

### Sommaire

- [Rapports des phases précédentes](#rapports-des-phases-précédentes)
- [Dépôt GitLab](#dépôt-gitlab)
- [Installation en local](#installation-en-local)
- [Dépendances](#dépendances)
- [Notice d'utilisation du site](#notice-dutilisation-du-site)
- [Routes](#routes)
- [Bugs connus](#bugs-connus)
- [Fonctionnalités non implémentées](#fonctionnalités-non-implémentées)
- [Retour d'expérience](#retour-dexpérience)

## Rapports des phases précédentes

[Rapport Phase 1 IHM](https://docs.google.com/document/d/1yN1q8FLshcoPevb3HeBBLGbJEP1rozqiiMuzPevZynI/edit?usp=sharing)

[Rapport Phase 2 Conception](http://madoc.univ-nantes.fr/mod/wiki/view.php?pageid=11511)

## Dépôt GitLab

ssh : `git@gitlab.univ-nantes.fr:E154706J/projet-genie-logiciel.git`

https : `https://gitlab.univ-nantes.fr/E154706J/projet-genie-logiciel.git`

## Installation en local

Pour installer le serveur sur votre machine, suivez ces instructions :
- Téléchargez le dépot GitLab et entrez dans le dossier nouvellement créé via les commandes suivantes :
```bash
git clone [addresse du dépôt GitLab]

cd ./projet-genie-logiciel
```
- Si sqlite3 est déjà installé sur votre machine et intégré dans votre variable d'environement $PATH, vous pouvez exécuter cette commande :
```bash
rm ./sqlite3*
```
- Installez les modules nécessaires au bon fonctionnement du serveur :
```bash
npm install
```
- Créez la base de données sqlite :
```bash
npm run createDB
```
- Si vous souhaitez insérer des données préconstruites dans la base de données, vous pouvez executer cette commande :
```bash
npm run fillDB
```
- Lancez le serveur :
```bash
npm start
```
Après cette commande, le serveur devrait être lancé en **localhost** sur le **port 8081**.
Si la variable d'environnement $PORT est définie sur un port spécifique pour accueillir le serveur, alors le serveur se lancera sur le port indiqué par cette variable.

## Dépendances

- bcrypt pour le hashage des mots de passe
- sqlite3 pour la base de données
- express et passport pour la gestion des routes et midlewares du serveur
- Bootstrap 4 et JQuery sont utilisés pour la partie client mais ne nécessitent aucune installation

## Notice d'utilisation du site

### En tant que nouvel utilisateur

#### Inscription

Pour vous inscrire, rendez-vous sur la page d'accueil :
- Cliquez sur "Pas encore inscrit ?".
- Complétez vos informations.
- **Attention :** Le mot de passe doit contenir au moins : 1 majuscule, 1 minuscule et 1 chiffre.

### En tant qu'utilisateur enregistré

#### Connexion

Pour vous connecter, rendez-vous sur la page d'accueil :
- Rentrez votre numéro étudiant et votre mot de passe
- Cliquez sur Se connecter ou appuyer sur la touche Entrée

#### Réserver un matériel

Une fois connecté, rendez-vous sur l'onglet Matériel :
- Cliquez sur le bouton "Reserver" du matériel souhaité. Une pop-up apparaît.
- Remplissez le créneau que vous souhaité réservé.
- Indiquez votre raison de la réservation (Soyez explicite, afin que l'administrateur de ce matériel accepte votre réservation)
- Appuyez sur le bouton "Réserver"

>  Vous pouvez désormais consulter votre réservation dans l'onglet "Réservation"

#### Réserver une salle

Une fois connecté, rendez-vous sur l'onglet Salle :
- Cliquez sur le bouton "Réserver" de la salle souhaité. Une pop-up apparaît.
- Remplissez le créneau que vous souhaité réservé.
- Indiquez votre raison de la réservation (Soyez explicite, afin que l'administrateur de ce matériel accepte votre réservation)
- Appuyez sur le bouton "Réserver"

>  Vous pouvez désormais consulter votre réservation dans l'onglet "Réservation"

#### Rechercher un matériel

Une fois connecté, rendez-vous sur l'onglet Matériel, sur votre gauche se trouve un champ de recherche :

- Le champ "Critère" permet la recherche d'un ou plusieurs mots dans le nom, les mots-clés, la description
- Lorsque vous cochez "disponibilité", vous pouvez rentrez un créneau souhaité
- Le tri peut s'effectuer par date de disponibilité (croissante/décroissante) ou par quantité (croissante/Décroissante)
- Vous pouvez également précisé le type de matériel recherché (informatique, instrument, mobilier, autre). 
  Le choix "..." signifique que vous rechercher tous type de matériel.


### En tant qu'administrateur

## Routes

### Routes des pages

### Routes de l'API

Toutes ces routes sont préfixées de `/api`.

> - GET /whoami/
>
> Permet de récupérer les données de profil de l'utilisateur connecté.

> - GET /logout/
>
> Permet à un utilisateur connecté de se déconnecter et de retourner à la page de connexion.

> - POST /utilisateur/register/
>
> Permet à l'utilisateur de s'inscrire sur le site en renseignant son numéro étudiant, son prénom, son nom et son mot de passe.

> - POST /utilisateur/login/
>
> Permet à un utilisateur enregistré de se connecter au site en renseignant son numéro étudiant et son mot de passe.

> - POST /utilisateur/bynum/
>
> Permet de récupérer les données d'un utilisateur via son numéro étudiant.

> - GET /utilisateur/getall/
>
> Permet de récupérer la liste des utilisateurs enregistrés dans le serveur.

> - POST /utilisateur/setadminrights/
>
> Permet modifier les droits administrateurs d'un utilisateur en précisant son numéro étudiant et un booléen lui donnant les droits ou non.

> - GET /notification/getall/
>
> Permet à un utilisateur de récupérer toutes les notifications le concernant (il devra faire une autre requête api si il veut plus d'informations sur les réservations correspondant à ces notifications).

> - POST /notification/seen/
>
> Permet à l'utilisateur de prévenir le serveur qu'il a vu une notification particulière.

> - GET /reservation/allbyuser/
>
> Permet à un utilisateur de récupérer toutes les réservations le concernant.

> - POST /reservation/getelem/
>
> Permet de récupérer les données de l'élément concerné par un réservation donnée.

> - POST /reservation/allbyid/
>
> Permet de récupérer une liste de réservations correspondant à une liste d'id de réservations fournis.

> - POST /reservation/allbyElem/
>
> Permet de récupérer la liste des réservations annexées à un élément particulier.

> - POST /reservation/validate/
>
> Permet à un administrateur de valider ou refuser une réservation donnée.

> - POST /reservation/submit/salle/
>
> Permet à un utilisateur de faire une demande de réservation de salle.

> - POST /reservation/submit/materiel/
>
> Permet à un utilisateur de faire une demande de réservation de matériel.

> - POST /creneau/byid/
>
> Permet de récupérer un créneau par son id.

> - POST /creneau/allbyid/
>
> Permet de récupérer tous les créneaux concernant un élément en particulier.

> - GET /creneau/getall/
>
> Permet de récupérer tous les créneaux de la base de données.

> - POST /element/byid/
>
> Permet de récupérer toutes les données d'un élément via son id.

> - GET /salle/getall/
>
> Permet de récupérer toutes les salles de la base de données.

> - POST /salle/add/
>
> Permet à un administrateur de rajouter une salle avec des créneaux et mots-clés associés.

> - POST /salle/delete/
>
> Permet à un administrateur de supprimer une salle et tous les créneaux, réservations et mot-clés associés de la base de données.

> - POST /salle/search/
>
> Permet de récupérer une liste de salles correspondant à certains critères spécifiques.

> - POST /salle/byid/
>
> Permet de récupérer une salle via son id.

> - POST /materiel/byid/
>
> Permet de récupérer un matériel via son id.

> - GET /materiel/getall/
>
> Permet de récupérer tous les matériels de la base de données.

> - POST /materiel/delete/
>
>Permet à un administrateur de supprimer un matériel et tous les créneaux, réservations et mot-clés associés de la base de données.

> - POST /materiel/search/
>
> Permet de récupérer une liste de matériels correspondant à certains critères spécifiques.

> - POST /materiel/add/
>
> Permet à un administrateur d'ajouter un matériel avec des créneaux et mots-clés associés.

## Bugs connus

- [ ] Dans les formulaires de critères de recherche de toutes les page en possédant un, le champ où on peut inscrire des caractères à chercher ne fonctionne pas pour la partie description d'un matériel ou d'une salle.

## Fonctionnalités non implémentées

- Dans la page /private/admin/administration.html, un administrateur est sensé pouvoir modifier un élément, matériel ou salle, mais nous n'avons pas eu le temps d'implémenter cette fonctionnalité.

- Dans les prototypes fournis dans la [phase IHM](https://docs.google.com/document/d/1yN1q8FLshcoPevb3HeBBLGbJEP1rozqiiMuzPevZynI/edit?usp=sharing) de ce sujet, on pouvait voir apparaître les matériels et salles déjà réservés par quelqu'un d'autre. Cela aurait impliqué un total remaniement de la base de données (qui était déjà bancale) fournie dans la [phase de conception](http://madoc.univ-nantes.fr/mod/wiki/view.php?pageid=11511) et un travail trop important sur les critères de recherches et l'affichage de leurs résultats.

- Dans les prototypes, un bouton message était affiché sur les éléments déjà réservés ou sur les notifications de demandes de réservations refusées. Ce bouton n'a pas été implémenté partiellement à cause du point précédent mais aussi parce qu'il aurait impliqué encore plus de modification de base de données et l'implémentation d'un système de messages jamais décrit dans la [phase de conception](http://madoc.univ-nantes.fr/mod/wiki/view.php?pageid=11511).

## Retour d'expérience

> Difficultés rencontrées : 
    
- Partie HTML/CSS : 
    - Difficulté pour correspondre au prototype créés lors de la première phase.
    - Création de multiple pop-up les uns sur les autres.
    - Création d'une première version du calendrier ainsi que d'un calendrier cliquable.
    
    Ces deux dernières difficultés nous ont imposées d'adapter la demande à nos capacités en favorisant les fonctionnalités lors de la création.
        
- Partie JavaScript: 
    - Obligation de refaire la base de données car celle fournie n'était pas adaptée.
    - Création du système de recherche de salle compliqué. Nous avons donc tenté de l'implémenter avec nos compétences.
    - Intégration du service sur le serveur distant. Cela nous a permis de nous apercevoir de l'importance de mettre les routes en relatif.

> Ce que nous avons appris : 

Durant ce projet, nous pour avons appris à mener un projet de développement.
Nous avons dû nous répartir les tâches en prenant en compte l'importance des tâches à effectuer et leur ordre.
Ce projet nous a aussi permis de développer nos compétences en HTML, CSS (notamment avec Bootstrap) et JavaScript.
Nous avons pu observer l'importance de l'adaptation. En effet nous devions sans arrêt adapter notre travail, ou celui effectué par les groupes précédents, en fonciton de nos capacités ou de la demande.
