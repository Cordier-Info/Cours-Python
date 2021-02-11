---
title: "TP6 : Projets"
chapter : false
weight : 5
---



# TP6 - Projets

*Lien vers le repository GitHub du TP : https://classroom.github.com/a/v7xsQyLB*



## Projet 1 : Jeu de Nim

Avec l'aide de la première partie de cette [vidéo](https://www.youtube.com/watch?v=2jahbr5wMHk) ou de toute autre source, découvrir l'algorithme de Bouton permettant de gagner au jeu de Nim.
Construire ensuite un programme qui :

- propose au joueur de construire le jeu de Nim qu'il souhaite (nombre de lignes et nombre de jetons par ligne),
- choisit de commencer ou non pour s'assurer une position gagnante (la machine doit gagner),
- laisse l'humain décider des jetons qu'il veut retirer (choix de la ligne, choix du nombre de jetons) lorsque c'est son tour puis joue de manière optimale lorsque c'est le tour de la machine…  Jusqu'à gagner,
- affiche la disposition des jetons à chaque tour.

Le corps du programme doit contenir (cf. `projet_1.py`) :

```Python
nim = initialise()
affiche(nim)
while sum(nim) != 0 :
    ns = nim_somme(nim)
    if ns == 0 :
        nim = tour_humain(nim)
    else :
        nim = tour_machine(nim,ns)
    affiche(nim)
print("Vous avez perdu...\n")
```

Reste à écrire les différentes fonctions...

![](/nimo.png)





## Projet 2 : Compression

Les fichiers image *portable bitmap file format*  `.pbm` sont extrèmement simples. C'est juste un texte ASCII qui comporte :

- un nombre magique indiquant le format : `P1`

- la largeur $L$ et la hauteur $H$ de l'image : `5 3` dans l'exemple
- puis une suite de $L\times H$ (= 15 dans notre cas) 1 et 0 correspondants à des pixels noirs ou blancs.

Le fichier `exemple.pbm` contient ainsi le texte :

```
P1
5 6
11111
10101
11111
10101
10001
11111
```

Et il ressemble à :

![](/exemple.png?width=400)

&nbsp;


#### Première mission :

Vous allez écrire un programme dans `projet_2a.py` qui convertit l'image jpeg couleur `Darwin.jpg` en fichier `.pbm`. Il faudra au préalable convertir chaque pixel de l'image d'origine en un pixel noir ou blanc (s'inspirer du cours).

Enregistrer le fichier créé sous le nom `imageNB.pbm` et le copier dans le repository.

Certes, ce format est simple et universel mais il a le défaut de prendre beaucoup plus de place mémoire que nécessaire. La raison en est l'utilisation de caractères texte pour encoder l'information. Les caractères `"1"` et `"0"` par exemple utilisent 8 bits plutôt que 1.

Mais l'objectif est d'aller plus loin que cette simple substitution en implémentant une réelle compression (quasi optimale) du fichier `imageNB.pbm` créé.

&nbsp;



#### Deuxième mission :

Commencer par lire  l'[article de Tangente](download/Tangente.pdf) sur l'**algorithme glouton** et/ou regarder [cette vidéo](https://youtu.be/yrOj8XvroIE).

Faire un premier programme `projet_2b.py` qui détermine les fréquences des différents caractères utilisés dans le fichier `imageNB.pbm` (`'0'`, `'1'`, `'P'`, `'7'`, `'9'`, `6`, `\n` et `' '`... Attention, le retour à la ligne et l'espace sont des caractères comme les autres).

Construire à la main l'arbre de Huffman pour ces 8 caractères en suivant la méthode indiquée dans l'article ou la vidéo et en déduire les 8 codes binaires qui remplaceront les 8 caractères dans le fichier compressé. Les noter dans le fichier `projet_2b.md`.

Construire un programme `projet_2c.py` qui remplace chaque caractère du fichier à compresser par son code binaire puis qui écrit ce code binaire dans un fichier de données `imageNB_comp.dat`.<br>Méthode pour écrire dans un fichier en binaire :

```python
f = open('imageNB_comp.dat','wb')
# s : chaîne de caractères obtenue en remplaçant chaque caractère
# du fichier original par son code issu de l'arbre
s = '1001110011...' 
# b est la transcription de ce code en bytes
b = bytes(int(s[i : i + 8], 2) for i in range(0, len(s), 8))
# puis on l'écrit dans f
f.write(b)
f.close()
```

Comparer et commenter les tailles des fichiers `imageNB.pbm` et  `imageNB_comp.dat`. <br>Comment se fait-il que le fichier jpeg de départ ait une taille comparable au fichier compressé alors qu'il s'agit d'une image couleur (émettre une ou des  hypothèses) ? <br>Vous noterez tout ça dans `projet_2c.md`.

Enfin, écrire un programme `projet_2d.py` qui décompresse `imageNB_comp.dat` en un fichier  `imageNB_decomp.pbm` et vérifier à sa taille qu'il n'y a pas eu perte d'information.

Méthode pour lire un fichier en binaire et récupérer le résultat sous la forme d'un chaîne de caractères constituée de `'1'` et de `'0'` :

```python
f = open('imageNB_comp.dat','rb')
code_bytes = f.read()
f.close()
code_texte = ''
for b in code_bytes :
    code_texte += format(b,'08b') # on obtient le texte codé (avec seulement des 1 et des 0)
```

