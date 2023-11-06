# Fonctionnement du Paléoscope

## A. Projet

Un projet est un espace sur lequel sont regroupées des scènes parmi lesquelles peuvent se déplacer des utilisateurs. Des médias peuvent également y être liés, accessibles depuis n’importe quelle scène du projet (documents, images, vidéos…).

### A.1 créer un nouveau projet sur le serveur

La première étape pour démarrer un projet est de le créer dans la base de données du Paléoscope via l'interface web. Pour l'instant cela se fait depuis le panneau CLI (ligne de commande, plus de détails en C.2.6) :

ouvrir un nouvel onglet ligne de commande

taper la commande`createproject NomDuProjet`

### A.2 Nouveau projet Unreal Engine

Pour créer un nouveau projet sur Unreal Engine 5 il faut télécharger le logiciel sur la plateforme Epic Games Launcher. Le Paléoscope est construit sur la version 5.2 du logiciel. Le projet est construit sur la base VR template qui offre une configuration de base et des préréglages optimisés pour la VR. Le projet est organisé en sous-dossiers (levels, materials, meshs, sequences, VFX, widgets etc.).

Les BluePrints (BP) sont un composant essentiel du développement sur Unreal Engine :  
« The Blueprint Visual Scripting system in Unreal Engine is a complete gameplay scripting system based on the concept of using a node-based interface to create gameplay elements from within Unreal Editor. As with many common scripting languages, it is used to define object-oriented (OO) classes or objects in the engine. » – Documentation Unreal Engine

Le projet est scindé en deux catégories d’acteurs : les acteurs indépendants et propres à l’environnement Unreal (le décor, les matériaux…) et les acteurs reliés au serveur (les échantillons, les beacons, VRPawn, écrans) qui lui transmettent et/ou reçoivent des informations sur les scènes.

La connexion au serveur se fait par l’intermédiaire du BluePrint BP\_GameInstance qui agit à l'échelle du projet et qui conserve donc les informations lors des changements de scène (level).

![](../archives/fondation-msh/_media/phase2/image2.png)  
Organisation du projet

![](../archives/fondation-msh/_media/phase2/image3.png)  
Websockets (détails du blueprint)

## B. Scène

Une scène se compose d’un modèle 3D qui peut contenir des animations, des balises, et peut être rejoint par des utilisateurs.

### B.1 Création du modèle 3D

Le Paléoscope permet de naviguer dans des échantillons réels. Ces échantillons sont obtenus grâce à la tomographie. Afin d’intégrer un échantillon dans un environnement 3D il faut effectuer une suite d’opérations consistant à changer le format et le poids du fichier. Les stacks d’images en .raw ne sont pas lisibles par les logiciels de 3D, et les fichiers sont souvent beaucoup trop lourds pour être manipulés tels quel. Le poids de l’échantillon et son format d’export diffère selon qu’il est destiné au web ou à la VR. A partir du fichier raw il est aussi possible de créer des rendus photoréalistes de l’échantillon.

#### B.1.1 Tomographie

La tomographie permet sans contact et sans destruction, de visualiser l’intérieur de la matière, par exemple les différentes couches d’un textile minéralisé. Cette technique d’imagerie utilisée en sciences et mécanique des matériaux permet d’analyser la microstructure des matériaux sans être intrusif et/ou destructif. La tomographie fournit une image tridimensionnelle à partir d’une série de radiographies via un calcul appelé la reconstruction.

#### B.1.2 Les exports

Le logiciel Unreal Engine 5, que l’on utilise pour développer la partie VR de l’écosystème, est capable de lire un nombre assez restreint de fichiers : mesh (OBJ ou FBX), voxel (VDB) ou nuage de points (E57). Nous favorisons les exports en format FBX car ils permettent d'exporter les textures et les animations rattachés à un échantillon. Pour intégrer des modèles 3D dans l’interface web il faut exporter des fichiers au format GLTF (.glb), cela nécessite de passer impérativement par un logiciel de 3D tel que Blender. Comme le FBX le fichier GLTF contient les textures et les animations du modèle.

![](../archives/fondation-msh/_media/phase2/image4.png)  
Schéma de conversion des données

Introduire toutes ces étapes de conversion dans le Paléoscope pourrait être une piste de développement.

#### B.1.3 Animations

Nous avons la possibilité d’associer des animations à nos modèles 3D, pour par exemple séparer les éléments d’un échantillon et le visualiser en éclaté (en VR et sur le web). La création d’une animation doit passer par un logiciel de 3D tel que Blender.

Il y a deux façons de créer une animation : 

1.  Associer un objet 3D (qui peut contenir plusieurs meshs) à une armature par l'intermédiaire de vertex groups et animer cette armature au moyen de keyframes.

2.  Animer plusieurs objets 3D séparés avec des keyframes.

Nous avons testé les deux techniques, la solution 1 avec l’armature est la plus adaptée car elle permet d’exporter une animation à la fois utilisable sur le web (GLTF/GLB) et sur Unreal Engine (FBX). Les utilisateurs verront alors exactement la même animation, que ce soit sur le web ou en VR.

![](../archives/fondation-msh/_media/phase2/image5.png)

#### B.1.4 Low-poly ou high-poly ?

Un objet 3D est composé de vertices (anglais pour sommets), des points ayant des coordonnées 3D (x, y, z) qui forment des segments et des surfaces. A partir du moment où l’on convertit les données du format .raw ou .vdb en mesh, le volume 3D est alors composé de vertices.  Le nombre de vertices va conditionner le poids du fichier. Pour optimiser les performances il est recommandé de réduire le nombre de vertices, pour avoir un modèle détaillé il faut l’augmenter :

1.  Le web supporte moins bien les gros fichiers, il faut donc limiter les modèles à environ 100 000 vertices.

1.  Unreal Engine 5, grâce au système d’optimisation Nanite, est capable de lire de très gros fichiers (dizaines de millions de vertices). Cependant il est recommandé de garder ce nombre relativement bas pour s’assurer des performances correctes en réalité virtuelle ( + ou - 1 million max).

Pour contrôler le nombre de polygone d’un objet 3D nous avons plusieurs possibilités : 

1.  la retopologie, cela consiste à venir modéliser un nouveau mesh par dessus le mesh high-poly en veillant à optimiser au maximum la géométrie. C’est un processus long et technique qui n’est pas adapté à des échantillons chaotiques.

1.  la décimation des vertices d’un mesh, on applique un modifier (blender) qui va supprimer un pourcentage défini des vertices de l’objet. C’est efficace mais pas très précis.

2.  la voxelisation, on voxelise le mesh de base grâce à un modifier (blender), c’est le procédé le plus efficace. 

En combinant ces différentes méthodes on peut obtenir de très bon résultats.

![](../archives/fondation-msh/_media/phase2/image6.png)

#### B.1.5 Matériaux 

Pour appliquer un matériau spécifique à un objet on peut soit utiliser un map UV soit se baser sur des paramètres plus ou moins hasardeux relatifs à l’objet.  
La création d’une map UV via le procédé d’*UV unwrapping* est adaptée aux modèles simples mais peut s’avérer dure, voire impossible pour des modèles très complexes tels que les échantillons tomographiques.  
Les systèmes de matériaux diffèrent selon les logiciels utilisés, l’utilisation d’un map UV et de textures bakées assure une bonne continuité sur les différents logiciels. Cette étape doit être réalisée sur Blender. Les modèles 3D ne pouvant pas être unwrappés doivent se voir appliquer au minimum un matériau avec une couleur et un smooth ou flat shading.

Une fois prêt, le fichier peut être exporté en .fbx pour Unreal Engine 5 et en .glb (GLTF) pour le web.

#### B.1.6 Rendus 3D

En important des fichiers VDB dans Blender on peut conserver les niveaux de gris de chaque voxel ainsi que des données colorées produites sur ParaView. On peut alors récupérer ces informations stockées sous forme d’attributs dans le fichier vdb, et les utiliser pour créer des textures.

En travaillant directement avec le fichier VDB on peut produire des images avec un niveau de détail plus important et moins gourmand en ressource qu’en utilisant des *meshs*.

Ces rendus (photoréalistes ou non), peuvent servir de documents support à l’expérience VR/Web en fournissant des images avec un niveau de détail impossible à obtenir en temps réel.

![](../archives/fondation-msh/_media/phase2/image7.png)

### B.2 Intégration au serveur

Une fois le modèle 3D exporté en format GLB, il faut le placer dans le code source du serveur (c'est une solution provisoire qui simplifie l'architecture technique du projet en stockant ces fichiers côté client, l'idée à l'avenir serait de pouvoir importer le modèle directement depuis l'interface web).

1.  dans le code source de paleoscope-v2-webclient créer un dossier dans /public/scenes et lui donner un nom (par exemple « nouvellescene »)

1.  renommer le fichier 3D « model.glb » et le placer dans le dossier nouvellement créé

2.  ajouter une image « thumbnail.png » dans ce même dossier qui représente l'échantillon

On peut ensuite créer la scène dans la base de données du Paléoscope via l'interface web. Pour l'instant cela se fait depuis le panneau CLI (ligne de commande) :

1.  ouvrir un nouvel onglet ligne de commande

2.  taper la commande`createscene NomDeLaScene nomdudossier largeur hauteur profondeur zoom` où`nomdudossier` est le nom défini dans l'étape 1,`largeur`,`hauteur` et`profondeur` sont les dimensions de la scène en centimètres (dimensions dans la VR, pas dans la réalité) et`zoom` est le grossissement de l'échantillon (300 pour une échelle 300:1)

Si tout s'est correctement passé, l'échantillon est maintenant créé et doit être visible dans le panneau de navigation dans les scènes.

### B.3 Intégration dans Unreal

Une fois le modèle exporté au format FBX il faut l’importer sur Unreal Engine 5. Si le modèle comporte des animations il faut l’importer en tant que skeletal mesh, sinon sous forme de static mesh.

1.  Importer le nouveau modèle dans le dossier mesh

1.  Dans le dossier level créer un nouveau level au nom de l’échantillon (ou dupliquer un ancien level pour conserver les paramètres de base).

2.  Créer un nouveau blueprint et glisser le mesh de l’échantillon (static ou skeletal) dans ce BP. On pourrait glisser directement le mesh dans la scène mais la création d’un blueprint permet plus de souplesse si l’on veut interagir avec l’échantillon, par exemple ajouter des animations etc…

3.  Attention, il ne faut pas toucher à l'échelle de l’échantillon. En effet, pour synchroniser parfaitement la VR et le web les modèles doivent être à la même échelle des deux côtés..

4.  En lançant la prévisualisation VR on peut maintenant naviguer dans et autour de l’échantillon.