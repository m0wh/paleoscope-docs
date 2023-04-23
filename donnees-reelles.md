# Un instrument de visualisation et de manipulation des données réelles

## 1. Constat

Il existe déjà de nombreux logiciels, payants ou open sources, qui permettent la lecture et la visualisation des données tomographiques (par exemple Fidji, Avizo ou 3D slicer).  
Ces logiciels ont l’avantage d’être utilisés par une large communauté d’utilisateurs, qui contribue à faire évoluer ces instruments en développant des plugins.  
Le logiciel 3D slicer dispose par exemple d’un plugin pour naviguer en VR dans l’échantillon étudié. Ces outils sont souvent développés pour le domaine médical.  

Ces logiciels ont la capacité d’importer et d’exporter une grande variété de formats de fichier, ce qui permet de transférer un échantillon d’un logiciel à l’autre pour en exploiter les particularités. On notera aussi qu’il est possible d’exporter des notes, points de repères et autres traces de recherche d’un logiciel à l’autre.

Dans ce contexte, il ne nous semble pas pertinent de développer un nouveau logiciel de recherche et de manipulation des données basé sur la réalité virtuelle. Les logiciels existent déjà, le plus efficace serait plutôt de développer un outil de visualisation et de phasage VR pour Fidji par exemple.

Les logiciels issus du monde du jeu vidéo tel que Unreal Engine sont conçus pour construire des expériences de jeu. A travers le développement d’interfaces graphiques, des intéractions avec l’environnement et un degré variable de scénarisation, le but est d’immerger le joueur dans un univers, et de l’y faire adhérer.

Les logiciels de traitement de données sont puissants et précis mais manquent cruellement d’affordance auprès des utilisateurs. Ils sont donc voués à être utilisés par des utilisateurs aguerris (chercheurs) et ne permettent pas d’être approchés par un public plus large.

## 2. Proposition

Nous proposons de créer un outil de visualisation et de manipulation basique des données tomographiques basé sur un système de réalité virtuelle partagée.  
Partagée car l’expérience vécue en VR est monitorée sur d’autres supports en temps réel (ordinateur, écran, téléphone…).  
Notre outil se situe en aval de la chaîne de traitement des données, nous n’envisageons pas, pour le moment, la possibilité de lire des fichiers raw et de les éditer en VR.  
Les opérations de marquage, seuillage, phasage auront été réalisées en amont sur les logiciels existants déjà performants. Le but de cet outil est de visualiser en VR l’échantillon et son phasage.

Une évolution de cet instrument serait de proposer des outils de phasage au sein même de la VR. Avec pourquoi pas une expérience de phasage en collaboration, avec un chercheur sur PC, qui sélectionne et identifie des slices et des points d’intérêt, et un autre dans la VR qui peint précisément les zones à phaser en bénéficiant de la vue en 3D.

## 3. Fonctionnalités de l’outil

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

 
