---
title : "Manipulation de fichiers"
chapter : false
weight : 6
pre : "<b>6. </b>"
---

# Manipulation de fichiers



## Interaction avec le système d'exploitation

Le module `os` offre la possibilité d'interagir avec le système d'exploitation indépendamment de la plateforme utilisée. 

 - `os.getcwd()` renvoie le répertoire courant (répertoire depuis lequel le programme est exécuté) sous forme de chaîne.


```python
import os

os.getcwd()
```

`'/Users/cordiermarc/Documents/prof/informatique/Python_6'`



- `os.chdir('répertoire')` permet de changer le répertoire courant pour le répertoire donné en argument. On peut soit donner le chemin absolu (qui commence par la racine, `/` sur un système Unix) 
  soit un chemin relatif (qui commence par `.` pour désigner le répertoire courant). 


```python
os.chdir('/Users/cordiermarc/Documents')
os.getcwd()
```

`'/Users/cordiermarc/Documents'`


```python
os.chdir('./prof/informatique/Python_6')
os.getcwd()
```

`'/Users/cordiermarc/Documents/prof/informatique/Python_6'`



- `os.listdir('répertoire')` permet de connaître le contenu d'un répertoire. Le nom raccourci du répertoire courant est `'.'`.


```python
os.listdir('.')
```


    ['.DS_Store',
     'puissances.txt',
     'images',
     'monfichier.rtf',
     'monfichier.txt',
     'cours6.ipynb',
     'ensoleillement.txt',
     '.ipynb_checkpoints']



- `os.path` est un sous-module qui propose plusieurs fonctions permettant de jouer avec les chemins d'accès et les noms de fichier. On en verra un exemple d'utilisation à la fin du document.

&nbsp;

&nbsp;



## Lecture et écriture de fichiers

Jusque-là, les différentes données de nos programmes étaient directement écrites dans le code et les sorties s'affichaient sur le shell.  

Mais il est souvent plus utile d'importer des données ou d'écrire les sorties dans des fichiers plutôt que sur l'écran. Pour cela, Python utilise l'objet `file`.

&nbsp;

&nbsp;



### Ouvrir et fermer un fichier

Un objet `file` est créé par l'utilisation de la fonction `open(nom du fichier,mode)` qui prend deux arguments.  


```python
f = open('monfichier.txt','w')
```

Le premier argument, *nom du fichier*, est une chaîne contenant le nom du fichier. Ce nom peut être donné avec le chemin d'accès absolu ou seulement l'arborescence relative au dossier dans lequel le programme est exécuté. 
En écrivant un nom sans chemin, le fichier se trouve dans le répertoire courant.

Le deuxième argument, *mode*, est une chaîne d'un ou deux caractères décrivant la façon dont le fichier est utilisé.  
*mode* peut être `r` quand le fichier n'est accédé qu'en lecture, `w` en écriture seulement (un fichier existant portant le même nom sera alors écrasé) 
et `a` ouvre le fichier en mode ajout (toute donnée écrite dans le fichier est automatiquement ajoutée à la fin). `r+` ouvre le fichier en mode lecture/écriture. L'argument mode est optionnel, sa valeur par défaut est `r`.  
`b` collé à la fin du mode indique que le fichier doit être ouvert en mode binaire c'est-à-dire que les données sont lues et écrites sous forme d'octets (type bytes). 
Ce mode est à utiliser pour les fichiers contenant autre chose que du texte.

Les objets `file` sont fermés grâce à la méthode `close()` : `f.close()` par exemple. Python ferme les fichiers automatiquement lorsque le programme se termine.

&nbsp;

&nbsp;



### Écrire dans un fichier

La méthode `write()` d'un objet `file` écrit une chaîne de caractères dans le fichier et renvoie le nombre de caractères inscrits. 


```python
f.write('Coucou monde !')
```

`14`

Plus pratique, la fonction native `print()` peut accepter en argument un objet `file`. Plutôt que d'être affichée sur le shell, la sortie de `print()` est alors redirigée vers ce fichier.


```python
print('\n', 35, 'Cl', 2, sep='', file=f)
f.close()
```



Exemple : le programme suivant écrit les quatre premières puissances de tous les entiers entre 1 et 1000, chaque champ étant séparé par une virgule, dans le fichier puissances.txt.


```python
fi = open('puissances.txt','w')
for i in range(1,1001) :
    print(i, i**2, i**3, i**4, sep=', ', file=fi)
fi.close()
```

&nbsp;

&nbsp;



### Lire un fichier

Pour lire `n` bytes d'un fichier, on utilise `f.read(n)`. En omettant `n`, tout le fichier est lu.  
`readline()` lit une seule ligne d'un fichier jusqu'au, en l'incluant, caractère `\n` de nouvelle ligne. Un nouvel appel de `readline()` lit la ligne suivante et ainsi de suite. `read()` et `readline()` renvoie toutes les deux une chaîne vide lorsque la fin du fichier est atteinte.  
Pour lire en une fois toutes les lignes dans une liste de chaînes, on utilise `f.readlines()`.

Les objet `file` sont itérables. On peut ainsi retourner chaque ligne d'un fichier une à une en utilisant une boucle :


```python
f = open('monfichier.txt')
for ligne in f :
    print(ligne, end='')
f.close()
```

    Coucou monde !
    35Cl2


Comme `ligne` contient déjà le caractère de nouvelle ligne lorsqu'elle est lue, on utilise `end = ''` pour empêcher `print` d'en ajouter un autre.  
Cette méthode de lecture ligne à ligne est à privilégier pour les gros fichiers à moins de vraiment vouloir contenir en mémoire l'ensemble du fichier.



Pour lire les nombres du fichier `'puissance.txt'` écrit précédemment, les colonnes doivent être converties en une liste d'entiers.  
Pour cela, chaque ligne doit être décomposée en ses différents champs et chaque champ explicitement converti en entier grâce à `int()` :


```python
fo = open('puissances.txt')
carrés, cubes, puiss4 = [],[],[]
lignes = fo.readlines()
fo.close()
for ligne in lignes :
    champs = ligne.split(',')
    carrés.append(int(champs[1]))
    cubes.append(int(champs[2]))
    puiss4.append(int(champs[3]))
n = 500
print(n, 'au cube vaut', cubes[n-1])
```

    500 au cube vaut 125000000

{{%notice note%}}

Mais en pratique, il vaut mieux utiliser les bibliothèques NumPy (2e semestre) ou Pandas pour des fichiers de données comme celui-ci.  
Vous apprendrez aussi à utiliser les méthodes des bases de données.

{{%/ notice%}}



---

Dans cet exemple, on va créer un petit gif qui illustre le théorème de La Hire :  

le programme produit un nouveau dossier `petitgif` dans lequel il crée 40 fichiers `svg` aux noms incrémentés (de `fig00.svg` à `fig39.svg`) décrivant des cercles et des segments.

Le `svg` pour Scalable Vector Graphics est un format de données ASCII, donc texte, conçu pour décrire des ensembles de graphiques vectoriels et basé sur le XML, un langage utilisant des balises `<...>`.

```Python
import math

nfigs = 40
# on crée un répertoire 'petigif' à partir du répertoire courant s'il n'existe pas déjà
rép_actuel = os.getcwd()
nv_rép = os.path.join(rép_actuel, 'petitgif') 
if not os.path.exists(nv_rép):  
    os.mkdir(nv_rép)                           
    
hauteur_cadre, largeur_cadre = 500, 500
# positions du centre du grand cercle :
cx, cy = hauteur_cadre / 2, largeur_cadre / 2
# rayons des trois cercles
r1, r2, r3 = 200, 100, 10

# liste d'angles pour faire tourner le petit disque :
alphas = [2*math.pi / nfigs * n for n in range(nfigs)]

for n, alpha in enumerate(alphas):
    filename = os.path.join(nv_rép, 'fig{:02d}.svg'.format(n))
    image = open(filename, 'w')   
    # En-tête du fichier SVG :
    print("""<?xml version="1.0" encoding="utf-8"?>
                 <svg xmlns="http://www.w3.org/2000/svg"
                      xmlns:xlink="http://www.w3.org/1999/xlink"
                      width="{}" height="{}" style="background: {}">""".format(hauteur_cadre, largeur_cadre, '#ffffff'), file=image)
    
    # grand cercle bleu :
    print('<circle cx="{}" cy="{}" r="{}" style="stroke: blue; stroke-width: 2px; fill: none;"/>'.format(cx, cy, r1),file=image)
    
    # grands diamètres 1 à 4 :
    print('<line x1="{}" y1="{}" x2="{}" y2="{}" stroke="blue" />'.format(cx,cy-r1,cx,cy+r1), file=image)
    print('<line x1="{}" y1="{}" x2="{}" y2="{}" stroke="blue" />'.format(cx-r1,cy,cx+r1,cy), file=image)
    print('<line x1="{}" y1="{}" x2="{}" y2="{}" stroke="blue" />'.format(cx+r1*math.cos(math.pi/4),cy+r1*math.sin(math.pi/4),cx-r1*math.cos(math.pi/4),cy-r1*math.sin(math.pi/4)), file=image)
    print('<line x1="{}" y1="{}" x2="{}" y2="{}" stroke="blue" />'.format(cx+r1*math.cos(-math.pi/4),cy+r1*math.sin(-math.pi/4),cx-r1*math.cos(-math.pi/4),cy-r1*math.sin(-math.pi/4)), file=image)
    
    # cercle rouge à l'intérieur du cercle bleu déplacé d'un angle alpha à chaque itération 
    cx2, cy2 = cx + (r1-r2) * math.cos(alpha), cy + (r1-r2) * math.sin(alpha)
    print('<circle cx="{}" cy="{}" r="{}" style="stroke: red; fill: none; "/>'.format(cx2, cy2, r2), file=image)
    
    cx3, cy3 = cx + r1 * math.cos(alpha), cy
    cx4, cy4 = cx , cy + r1 * math.sin(alpha)
    cx5, cy5 = cx + r1 * math.cos(alpha+math.pi/4)*math.cos(math.pi/4), cy - r1 * math.cos(alpha+math.pi/4)*math.sin(math.pi/4)
    cx6, cy6 = cx + r1 * math.sin(alpha+math.pi/4)*math.cos(math.pi/4) , cy + r1 * math.sin(alpha+math.pi/4)*math.sin(math.pi/4)
    
    # petits diamètres 1 et 2 :
    print('<line x1="{}" y1="{}" x2="{}" y2="{}" stroke="red" />'.format(cx3,cy3,cx4,cy4), file=image)
    print('<line x1="{}" y1="{}" x2="{}" y2="{}" stroke="red" />'.format(cx5,cy5,cx6,cy6), file=image)
    
    # 4 petits disques :  
    print('<circle cx="{}" cy="{}" r="{}" style="stroke: purple; fill: purple;"/>'.format(cx3, cy3, r3), file=image)
    print('<circle cx="{}" cy="{}" r="{}" style="stroke: purple; fill: purple;"/>'.format(cx4, cy4, r3), file=image)
    print('<circle cx="{}" cy="{}" r="{}" style="stroke: purple; fill: purple;"/>'.format(cx5, cy5, r3), file=image)
    print('<circle cx="{}" cy="{}" r="{}" style="stroke: purple; fill: purple;"/>'.format(cx6, cy6, r3), file=image)
    print('</svg>', file=image)
```

On peut utiliser ensuite le logiciel libre [ImageMagick software](https://imagemagick.org/index.php) qui permet de créer un gif à partir d'une série d'images via la ligne de commande (une fois dans le répertoire *petitgif*) :<br>`convert -delay 5 -loop 0 fig*.svg animation.gif`

![](/animation.gif)

&nbsp;

&nbsp;



## Fichiers image

Grâce à la librairie PIL (python imaging library) Python permet aussi de manipuler des fichiers image.

Les fonctions de ce module permettent d'avoir accès aux pixels d'une image par leurs coordonnées cartésiennes (*colonne*,*ligne*) :


```python
from PIL import Image

image = Image.open('images/Darwin.jpg')
largeur, hauteur = image.size
print('largeur : {} pixels, hauteur : {} pixels'.format(largeur,hauteur))
```

`largeur : 700 pixels, hauteur : 967 pixels`

```python
pixels_image = image.load()
pixels_image[23,102]
```

`(90, 78, 66)`

{{%notice info%}}
Chaque pixel contient un tuple de 3 éléments codant sa couleur au format RGB : chacune des 3 couleurs primaires, rouge, vert et bleu, est codée par un byte de 8 bits autorisant donc 256 valeurs (0 pour le noir, 255 pour la couleur saturée). Cela fait en tout une palette de $256^3$ soit plus de 16 millions de couleurs.
{{%/ notice %}}

Supposons que l'on souhaite transformer une photo en couleur en une photo noir et blanc (ou plutôt en niveaux de gris).

On peut commencer par définir une fonction `intensité_moyenne(pixel)` qui fait la moyenne des intensités des 3 couleurs de chaque pixel. Puis on affecte cette valeur unique à chacune des intensités des 3 couleurs dans une nouvelle image (cela donne une teinte plus ou moins foncée de gris).


```python
def intensité_moyenne(pixel) :
    Imoy = (pixel[0]+pixel[1]+pixel[2])/3
    return int(Imoy)

image_NB = Image.new("RGB", (largeur, hauteur), "black")
pixels_image_NB = image_NB.load()
for i in range(largeur) :
    for j in range(hauteur) :
        Imoy = intensité_moyenne(pixels_image[i,j])
        pixels_image_NB[i,j] = (Imoy,Imoy,Imoy)

print(pixels_image[23,102],pixels_image_NB[23,102])
image_NB.save('images/Darwin_N&B.jpg')
```

`(90, 78, 66) (78, 78, 78)`


![](/resultat.jpg)



On peut aussi créer une image à partir de rien comme dans cet exemple où la couleur des pixels dépend de leurs positions :


```python
img = Image.new( 'RGB', (250,250), "black") 
pixels = img.load() 
for i in range(img.size[0]):    
    for j in range(img.size[1]):    
        pixels[i,j] = (i, j, 100) 
img
```



![](/output_52.png)

&nbsp;

&nbsp;



## Interaction avec l'utilisateur : la fonction `input()`

La plupart des scripts élaborés nécessitent à un moment ou à un autre une intervention de l'utilisateur (entrée d'un paramètre, clic de souris sur un bouton, etc.). Dans un script en mode texte (comme ceux que nous avons créés jusqu'à présent), la méthode la plus simple consiste à employer la fonction native `input()`. Cette fonction provoque une interruption dans le programme courant. L'utilisateur est invité à entrer des caractères au clavier et à terminer avec `<Enter>`. Lorsque cette touche est enfoncée, l'exécution du programme se poursuit, et la fonction fournit en retour une valeur correspondant à ce que l'utilisateur a entré. Cette valeur peut alors être assignée à une variable quelconque.  

Si un argument est donné, il est affiché à l'écran :

```python
print("Quel est votre film préféré ?")
s = input('-->')
```

`Quel est votre film préféré ?`

`-->` **La Vie de Brian**

```python
s
```

`'La Vie de Brian'`



`input()` convertit ce qui a été entré au clavier en chaîne de caractères. Si on attend d'autres types de données, il faut utiliser les fonctions de conversion `int()` ou `float` :

```python
a = int(input('Choisir un chiffre :'))
a*2
```

`Choisir un chiffre :` **4**

`8`

```python
a = float(input('Choisir un chiffre :'))
a*2
```

`Choisir un chiffre :` **2**

`4.0`

&nbsp;

&nbsp;



## Récupérer des données sur le web

Exemple de programme :

```python
import requests
import matplotlib.pyplot as plt
import matplotlib.dates as mdates
from dateutil.parser import parse

dep = input("Numéro du département ? ")

# données gouvernementales covid
url = "https://www.data.gouv.fr/fr/datasets/r/63352e38-d353-4b54-bfd1-f1b3ee1cabd7"
download = requests.get(url)
brut = download.content.decode('utf-8') # pour transformer les bytes récupérés en string
lignes = brut.split('\n')
date, hosp = [],[]
for ligne in lignes[1:-1:3] : # on saute l'en-tête et ne garde que les sexes 0 correspondant à la somme féminin+masculin
    champs = ligne.split(';')
    if champs[0] == '"{}"'.format(dep) :
        date.append(parse(champs[2].strip('"'))) # parse() sert à convertir la chaîne de caractères en une date
        hosp.append(int(champs[4]))

# liste noms des départements
url2 = "https://static.data.gouv.fr/resources/departements-et-leurs-regions/20190815-175403/departements-region.csv"
download2 = requests.get(url2)
brut2 = download2.content.decode('utf-8')
lignes2 = brut2.split('\n')
for li in lignes2 :
    ch = li.split(',')
    if ch[0]==str(dep) :
        nom_dep = ch[1]

fig, ax = plt.subplots(figsize=(15,10))
ax.plot(date,hosp)
plt.title("Patients Covid en réa en {}".format(nom_dep), fontsize=16)
ax.xaxis.set_major_formatter(mdates.DateFormatter('%d/%m'))
ax.xaxis.set_major_locator(mdates.DayLocator(interval=10))
fig.autofmt_xdate()
plt.show()
```

![covid17](/covid17.png)

