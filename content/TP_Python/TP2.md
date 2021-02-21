---
title : "TP2 : Bases et Chaînes"
chapter : false
weight : 1
---

# TP2 : Cours 1 et 2

*Lien vers le repository GitHub du TP : https://classroom.github.com/a/Prcpdubn*



## Exercice 1

Expliquer le résultat surprenant du code suivant dans `exo_1.md` :


```python
d = 8
e = 2
from math import *
sqrt(d ** e)
```

`16.88210319127114`

&nbsp;



## Exercice 2

Combien de fois une feuille de papier d'épaisseur $e = 0,1$ mm doit-elle être pliée pour atteindre la Lune&nbsp;?

Écrire dans `exo_2.py` un script Python qui calcule et imprime la réponse sans utiliser de boucle.

&nbsp;

&nbsp;



## Exercice 3

Le world geodesic system (WGS) ou système géodésique mondial établit des références pour les coordonnées et dimensions du globe utilisées par le système de positionnement par satellite GPS.  
Dans sa version WGS-84, la géoïde terrestre est approximée par un ellipsoïde de révolution aplati dont le demi grand axe $a$ et le demi petit axe $c$ vallent :

$a = 6378137,0\text{ m}$

$c = 6356752,314245\text{ m}$.

La formule donnant la surface d'un sphéroïde aplati est :

$ S=2\pi a^2\left(1+\frac{1-e^2}{e}\text{artanh}(e)\right) $ avec $e^2=1-\frac{c^2}{a^2}$

Utiliser cette formule dans un script Python (`exo_3.py`) pour déterminer et imprimer la superficie de la Terre et comparer au résultat obtenu en approximant la Terre comme une sphère de rayon 6371 km.

![img](/wgs.png?width=400)




## Exercice 4

Écrire dans `exo_4.py` une expression d'une seule ligne permettant de déterminer si une chaîne de caractère est un **palindrome**.

&nbsp;



## Exercice 5

Les variables suivantes ont été définies dans `exo_5.py`  :


```python
k = 1.380649E-23
k_unité = 'J/K'

e = 1.602176634E-19
e_unité = 'C'

N_A = 6.02214076E23
N_A_unité = 'mol-1'

c = 299792458
c_unité = 'm/s'
```

Compléter le code pour afficher les résultats ci-dessous (<u>utiliser la méthode de formattage</u>) :

`e = 0.0000000000000000001602176634 C`

`k = 1.381e-23 J/K`

`N_A = 602214075999999987023872 mol-1`

`c = 000299792458 m/s`

