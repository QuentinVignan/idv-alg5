# Monet Maker

Le projet Monet Maker a pour but d'expérimenter les bibliothèques de traitement d'images au travers de l'algorithmie. Diverses étapes sont mises en place pour l'expérimentation :

1. Pré-processing de l'image. La première étape, appelée Big Fernand Léger, récupère les niveaux de gris d'une image et détoure ses contours à l'aide de l'algorithme de détection des bords conçu par John F. Canny. Puis affine les contours par seuillage d'image (Thresholding), une méthode permettant de remplacer les niveaux de gris et ressortir une image binaire déterminant un ensemble de pixels selon une valeur seuil.
2. Pré-processing de l'image: Gestion des détails. La deuxième étape, appelée Sale Vador Dali, approfondit le traitement des détails de l'image par l'utilisation d'un flou. Trois flous ici sont mis en place, flou classique, flou gaussien et flou médian.
   1. Flou classique: Le flou classique supprime le contenu à haute fréquence, comme les bords, de l'image et la rend plus lisse.En général, le flou est obtenu par convolution (chaque élément de l'image est ajouté à ses voisins locaux, pondérés par le noyau) de l'image à travers un noyau de filtre passe-bas. (Source: TutorialPoint OpenCV)
   2. Flou gaussien: L'image est convoluée avec un filtre gaussien au lieu du filtre en boîte. Le filtre gaussien est un filtre passe-bas qui supprime les composantes à haute fréquence. (Source: TutorialPoint OpenCV)
   3. Flou médian: l'élément central de l'image est remplacé par la médiane de tous les pixels de la zone du noyau. Cette opération permet de traiter les bords tout en supprimant le bruit. (Source: TutorialPoint OpenCV)
3. Rendu de l'image. La troisième étape, appelée Zhang GUI, récupère les contours isolés de l'image pour les dessiner à l'écran. Nous utilisons TurtlePython pour transformer les les pixels noirs de l'image binaire au thresholding et les faire apparaître à l'écran. Le programme dessine de haut en bas et rafrachit selon un nombre de pixels donné.
4. Rendu de l'image, humanisé. La quatrième étape, appelée Renoir Et Blanc, va depuis les contours de l'image déjà récupérés établir un k-d tree, qui servira à déterminer diverses manières de mettre en relation les pixels à dessiner. L'objectif est de dessiner via ce k-d tree les différents pixels en formant des lignes davantage humaines. Il faut abandonner le style "impression" de l'étape précédente, pour faire du trait par trait.
5. Rendu de l'image. La cinquième étape, appelée Paulychrome Gauguin, va depuis le k-d tree de l'étape précédente ajouter des couleurs. Le but sera de d'analyser les couleurs de l'image, pour en récupérer une palette et redessiner l'image coloriée en plus des contours.

## Dépendances

### OpenCV

Si Scikit était un choix possible pour l'analyse d'image, OpenCV est un outil utilisé beaucoup plus largement par la communauté. Là où scikit offre des possibilités non implémentées par OpenCV dans le traitement d'images, tel que le filtering, la morphologie, la transformation, la conversion de couleur etc... OpenCV offre une documentation plus large grâce à son utilisation répandue et des possibilités plus grandes de recherche autour des concepts implémentés, de sorte à pouvoir les remettre en question.

Dans le cas du projet Monet Maker, les features supplémentaires offertes au sein de Scikit ne sont pas obligatoires, ni spécialement utiles, pour cette expérimentation.

Aussi, ceci étant un projet d'expérimentation algorithmique plus que de réalisation d'un outil extrêmement poussé de modification d'images, le choix OpenCV de l'ouverture à la documentation et aux ressources a été fait contre les features de Scikit.


Sources:
- https://stackshare.io/stackups/opencv-vs-scikit-image
- https://medium.com/analytics-vidhya/opencv-vs-skimage-for-image-analysis-which-one-is-better-e2bec8d1954f


### TurtlePython

TurtlePython est un outil de dessin trait par trait. Matérialisé sous la forme d'une tortue représentant un stylo posé sur une feuille, que l'on peut guider à l'aide de fonctions, de ses mouvements aux actions de descente et levée de stylo. 

L'objectif final du projet étant de réaliser un dessin dessiné à la main, comme le ferait un artiste en temps réel, la librairie s'est imposée comme choix d'or pour la réalisation du dessin.

De même, la librarie cible le dessin en temps réel, parfaitement adapté, permettant d'omettre d'autres libraries GUI beaucoup plus poussées, lourdes et offrant d'autres features qui ne seront pas utilisés sur le projet, tel que Tkinter.

En autres, TurtlePython, importe lui-même les morceaux de librairies nécessaires à son utilisation directe.


### Argparse

De manière à personnaliser l'expérience de l'utilisateur, la librairie Argparse a été choisie, simple d'utilisation et utile pour l'implémentation de flags de lancement de programme Python. Ainsi, on peut personnaliser les valeurs de filtre utilisées par les différentes étapes du projet.


### Matplotlib

Nécessaire pour l'affichage de PythonTurtle, la librairie est installée pour résoudre les soucis d'affichage lors de l'utilisation d'un mac m1 et peut être supprimé à la main des fichiers requirements.txt sans impact lors de l'utilisation de distributions hautes basées sur Debian Linux.


### Scipy

Utilisé pour le Machine Learning Python, Scipy apporte en autres les outils facilité d'utilisation d'algorithme NNS et d'objets KDTree. De sorte à éviter d'avoir à réimplémenter une classe de k-d tree, nous utilisons cet outils pour nous assurer de la viabilité de la méthode et faciliter son utilisation. Aussi les calculs de distance et de voisin le plus proches étant intégrés, nous pouvons nous intéresser à la logique de traitement.


## Installation du projet


Le projet utilise Python3 et les dépendances sont à récupérer sur Ubuntu/macOS via cette commande:

`python3 -m pip install -r ./requirements.txt`

## Lancement du projet

Le projet se lance à l'aide de la commande suivante:

`python3 main.py`

Des flags additionnels sont précisés dans les readme des différentes étapes.