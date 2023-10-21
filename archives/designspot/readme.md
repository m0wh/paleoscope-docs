# DesignSpot

## Un instrument de visualisation et de manipulation des données réelles

### 1. Constat

Il existe déjà de nombreux logiciels, payants ou open sources, qui permettent la lecture et la visualisation des données tomographiques (par exemple Fidji, Avizo ou 3D slicer).  
Ces logiciels ont l’avantage d’être utilisés par une large communauté d’utilisateurs, qui contribue à faire évoluer ces instruments en développant des plugins.  
Le logiciel 3D slicer dispose par exemple d’un plugin pour naviguer en VR dans l’échantillon étudié. Ces outils sont souvent développés pour le domaine médical.  

Ces logiciels ont la capacité d’importer et d’exporter une grande variété de formats de fichier, ce qui permet de transférer un échantillon d’un logiciel à l’autre pour en exploiter les particularités. On notera aussi qu’il est possible d’exporter des notes, points de repères et autres traces de recherche d’un logiciel à l’autre.

Dans ce contexte, il ne nous semble pas pertinent de développer un nouveau logiciel de recherche et de manipulation des données basé sur la réalité virtuelle. Les logiciels existent déjà, le plus efficace serait plutôt de développer un outil de visualisation et de phasage VR pour Fidji par exemple.

Les logiciels issus du monde du jeu vidéo tel que Unreal Engine sont conçus pour construire des expériences de jeu. A travers le développement d’interfaces graphiques, des intéractions avec l’environnement et un degré variable de scénarisation, le but est d’immerger le joueur dans un univers, et de l’y faire adhérer.

Les logiciels de traitement de données sont puissants et précis mais manquent cruellement d’affordance auprès des utilisateurs. Ils sont donc voués à être utilisés par des utilisateurs aguerris (chercheurs) et ne permettent pas d’être approchés par un public plus large.

### 2. Proposition

Nous proposons de créer un outil de visualisation et de manipulation basique des données tomographiques basé sur un système de réalité virtuelle partagée.  
Partagée car l’expérience vécue en VR est monitorée sur d’autres supports en temps réel (ordinateur, écran, téléphone…).  
Notre outil se situe en aval de la chaîne de traitement des données, nous n’envisageons pas, pour le moment, la possibilité de lire des fichiers raw et de les éditer en VR.  
Les opérations de marquage, seuillage, phasage auront été réalisées en amont sur les logiciels existants déjà performants. Le but de cet outil est de visualiser en VR l’échantillon et son phasage.

Une évolution de cet instrument serait de proposer des outils de phasage au sein même de la VR. Avec pourquoi pas une expérience de phasage en collaboration, avec un chercheur sur PC, qui sélectionne et identifie des slices et des points d’intérêt, et un autre dans la VR qui peint précisément les zones à phaser en bénéficiant de la vue en 3D.

### 3. Fonctionnalités de l’outil

En VR : 
- navigation autour et dans l’échantillon
- manipulation de l’orientation et de l’échelle de l’échantillon
- importation et ajout, de balises et de repères dessinés
- possibilité de sélectionner des slices

Sur les moniteurs : 
- visualisation et choix de l’échantillon
- suivi en temps réel du déplacement de l’opérateur VR : 
- suivi sur un modèle 3D
- suivi sur une visualisation et coupe du modèle
- importation et ajout, de balises et de repères dessinés

## Un instrument de communication d’une recherche, liée à un échantillon particulier, qui s’adapte à différentes situations de médiation

### 1. Constat

La communication d’une recherche scientifique donnée se fait le plus souvent par l’intermédiaire d’un article scientifique. Cet article est un pdf constitué de blocs de textes, d’images et de liens. Il peut être facilement stocké, partagé et imprimé.  
Il devient cependant tout de suite moins pratique lorsqu’il s’agit de faire communiquer plusieurs recherches entre elles ou encore s’adresser à un public. Le format linéaire du pdf est adapté à la lecture mais pas vraiment à la déambulation et la découverte d’une recherche.  
De plus, quand il s’agit d’une recherche liée à des objets physiques le pdf ou le power point détachent de la physicalité de l’objet et rend le sujet relativement abstrait.  

### 2. Proposition
Nous proposons de créer un outil de visualisation et de navigation dans la recherche, basé sur l’échantillon.  
L’échantillon, déjà étudié et traité, est intégré au logiciel de découverte. On peut alors choisir différents layers d’information, naviguer dans l’échantillon, sélectionner des éléments et afficher des points d’interprétation.  
L’objectif est de formaliser la recherche sous la forme d’une expérience immersive et intéractive.  

Les données visualisées ne seront pas les données brutes, ce sera des morceaux extraits de la donnée brute, transformés le plus souvent en mesh, parfois re-modélisés, animés, simplifiés ou augmentés, selon les besoins.  


### 3. Fonctionnalités de l’outil 

Navigation en VR dans l’échantillon
- interaction avec les points d’intérêt
- ajout de balises
- ajout d’annotations dessinées
- capture et partage photographique
- prise de mesure
- perception multisensorielle

Interface web AR
- affichage de l’échantillon en réalité augmentée pour percevoir son échelle réelle. 
- mise à jour des layers de visibilité

Interface web bureau
- suivi des opérateurs VR en temps réel dans l’échantillon ( affichage 3D ou slice)
- accès aux articles scientifiques associés
- partage d’infos et de médias avec les opérateurs VR
- sélections des layers d’information à afficher
- ajout de balises
- ajout d’annotations dessinées
- téléportation des opérateurs VR dans l’échantillon 3D

## Infrastructure technique du paléoscope

### Paléoscope V1

La première version du paléoscope réalisée lors de l'Atelier de Projet "Paléoinspiration" à l'ENSCI–Les Ateliers en 2021 reposait sur une infrastructure en local :
- Les barres de contrôle : un gros controlleur MIDI Arduino manipulable
- Un casque de VR (HTC Vive) dans laquelle un utilisateur explorait les scènes
- Un PC central qui faisait tourner Unreal Engine, réagissant aux signaux MIDI

![Schéma technique du paléoscope V1](_media/schema-tech-V1.jpg)

### Paléoscope V2

Le paléoscope V2 revoit complètement son fonctionnement en se basant sur une architecture serveur centralisée.

Les clients (utilisateur VR, smartphone, site web, objet connecté…) se connectent à un échantillon sur le serveur qui leur envoie les informations dont ils ont besoin (géométrie, balises, notes, medias…). Ils peuvent ensuite envoyer des messages au serveur (par exemple à la création d'une nouvelle balise, au déplacement…) qui le transmettra à tous les autres clients en temps réel grâce aux websockets.

![Schéma technique du paléoscope V2](_media/schema-tech-V2.jpg)

Cette architecture permet de concevoir beaucoup plus rapidement des dispositifs variés et sur mesure. Elle présente aussi l'avantage considérable de fonctionner en ligne et donc supprimer les contraintes matérielles (connectique…) et géographiques (les clients peuvent se retrouver dans l'échantillon en temps réel partout dans le monde).
