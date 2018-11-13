# Projet CORBA : Simulation Suivi GPS/GSM


## I. Contexte de l’application à réaliser

Le but de ce projet est de réaliser l’application CORBA régissant un processus de suivi de livraison
via un système GPS (Global Positionning System) et GSM (Global System for Mobile
communications) simplifié. Dans ce système, les satellites diffusent leur position aux terminaux
mobiles. Chaque terminal a besoin de 3 satellites pour identifier sa position. Ensuite, un terminal
utilise le GSM pour envoyer sa position à un système de collecte. Les clients peuvent ensuite
interroger le système de collecte pour obtenir un historique de la position d’un ou plusieurs terminaux
mobiles.
Cette application se compose d’une partie frontend représentant l’utilisation de la plate-forme de
localisation par des clients et d’une partie backend représentant le fonctionnement interne du système.

## II. Réalisation du backend
Le système GPS se compose :

* D’un ensemble de satellites. Pour simplifier, les satellites ont une orbite géostationnaire, c’està-dire
qu’ils sont immobiles pour un observateur terrestre. Toutefois, l’attraction terrestre leur
fait perdre peu à peu leur altitude et les fait bouger de leur position. Pour éviter cela, chaque
satellite dispose d’un moteur-fusée lui permettant de réajuster sa position (altitude et position).
Chaque satellite possède un émetteur et un récepteur embarqué. Le terminal mobile récepteur
des données satellites n’étant pas très puissant, seules les stations de base ou stations-relais
peuvent envoyer des données aux satellites.
Les satellites envoient leur identifiant ainsi que leur position périodiquement aux terminaux du
système qui y sont abonnés.
* De stations terrestres. Les stations terrestres peuvent communiquer avec des satellites. Il y a
deux types de stations :
  * Stations de base GPS. Une station de base est un gestionnaire de satellite. Elle peut
commander un positionnement au satellite.
  * Stations-relais GPS. Comme le nombre de stations de base est TRÈS limité et que les
satellites sont uniformément répartis autour de la terre, les stations de base ne peuvent
gérer toutes les communications avec tous les satellites. Il faut dans ce cas utiliser des
stations-relais pour joindre les satellites concernés. Les stations-relais sont en nombre
quelconque et sont réparties sur la planète. Leur seul but est de retransmettre aux
satellites de leur rayon d’action, les messages de télécommande de la station de base.

Le système GSM se compose d’un ensemble de stations de base GSM réparties, elles aussi, sur la
planète. 
Les stations de base GSM gèrent la communication entre les terminaux mobiles et le réseau
téléphonique commuté (pour simplifier on ne s’occupera que de l’envoi de messages textes de type
SMS). 
Les terminaux mobiles doivent pouvoir envoyer des SMS à d’autres terminaux mobiles et à des
terminaux fixes et vice versa.

## III. Réalisation du front end et gestion des terminaux mobiles 
Maintenant, on souhaite commercialiser le système de collecte. 
Pour cela, il faut ajouter au système du
I, un lien applicatif entre un terminal mobile et le système de collecte.

Le système de collecte gère un ensemble de terminaux mobiles identifiés par un numéro SIM et un
numéro de téléphone. Son rôle est de collecter régulièrement les positions de chaque terminal mobile et de les archiver. Le système peut aussi modifier la période de collecte pour chaque terminal mobile
et les désactiver à distance (la réactivation devra être réalisée manuellement) via l’envoi de SMS.


Pour utiliser ce système GPS/GSM, les terminaux doivent effectuer deux opérations :
* En premier, ils doivent s’authentifier auprès d’une station de base GSM en fournissant un
identifiant SIM.
* Dans un second temps, ils doivent envoyer régulièrement (selon la période choisie par le
système de collecte), via la station de base GSM, leur position ainsi que leur identifiant SIM
au système de collecte (cet envoi se fait en utilisant des SMS – le numéro de téléphone du
système de collecte est précisé lors de l’initialisation du terminal mobile).
* Lorsqu’ils changent de cellule GSM, les terminaux devront à nouveau s’authentifier avec leur
identifiant SIM.

## IV. Réalisation d’une application de suivi de flotte
On souhaite faire évoluer le système en proposant aux entreprises, un suivi des positions des différents
terminaux les concernant. Les entreprises clientes, après authentification, doivent pouvoir interroger
l’application afin de connaître les différents relevés de position de leur flotte.


## V. Travail demandé
### Partie I : Conception du contrat IDL de l’application
Concevez et rédigez le contrat IDL de l’application permettant de répondre aux spécifications
précédemment énoncées. Constituez un dossier qui, outre le contrat IDL, comportera :
* Les diagrammes UML adéquats exprimant le résultat de l’analyse de cette application.
* Les différentes catégories d’entités logicielles en identifiant leur rôle et leur positionnement
envisagé sur l’environnement technologique cible.
* Les interactions pouvant survenir entre ces types d’entités.

