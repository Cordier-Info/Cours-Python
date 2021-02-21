---
title: "TP5 : Fonctions et Fichiers"
chapter : false
weight : 4
---



# TP5 : Fonctions et Fichiers

*Lien vers le repository GitHub du TP : https://classroom.github.com/a/qRVUwdoz*



## Exercice 1

Le code suivant essaye de calculer le solde d'un compte épargne ayant un taux d'intérêt de 5% et un solde initial de 100 € après quatre années.


```python
solde = 100
def ajoute_intérêt(solde,taux) :
    solde += solde * taux/100
    
for année in range(4) :
    ajoute_intérêt(100,5)
    print('Solde après l\'année {} : {:.2f} €'.format(année+1,solde))
```

    Solde après l'année 1 : 100.00 €
    Solde après l'année 2 : 100.00 €
    Solde après l'année 3 : 100.00 €
    Solde après l'année 4 : 100.00 €


Expliquer pourquoi cela ne marche pas et trouver une alternative (`exo_1.md` et `exo_1.py`)

Question subsidiaire : dans Futurama, Fry a été cryogénisé alors qu'il avait 93 cts sur son compte en banque. 1000 ans plus tard, il retourne dans sa banque. Combien lui ont rapporté les 2,25% d'intérêt ?<br>Faire afficher le résultat par `exo_1.py`.



![](/Fry.jpeg)



## Exercice 2

La portée d'un projectile lancé avec un angle $\alpha$ et une vitesse $v$ depuis le sol sur un terrain plat vaut (si on néglige les frottements, la courbure et la rotation de la Terre) :<br>
$d = \frac{v^2 \sin 2\alpha}{g}$<br>
où $g$ est la pesanteur ($g = 9,81\text{ m.s}^{-2}$).<br>
La hauteur maximale atteinte par le projectile (la flèche) est :<br>
$h = \frac{v^2 \sin ^2 \alpha}{2g}$

Écrire dans `exo_2.py` une fonction qui renvoie la portée et la hauteur atteinte par un projectile en prenant $\alpha$ et $v$ en argument.
Tester la fonction pour $\alpha = 30°$ et $v=10\text{ m.s}^{-1}$.

&nbsp;



## Exercice 3

Écrire dans `exo_3.py` deux fonctions prenant chacune en argument deux listes de trois nombres représentant les coordonnées de deux vecteurs et qui renvoient le **produit scalaire** 
et le **produit vectoriel** de ces deux vecteurs.

&nbsp;



## Exercice 4

Écrire dans `exo_4.py` un testeur de tautologie :

- Écrire d'abord une fonction `rel_1(a,b)` (de signature `rel_1(bool,bool)`$\rightarrow$ `bool`) qui retourne $\neg(a\lor b)$ et une fonction `rel_2(a,b)` (de signature `rel_2(bool,bool)`$\rightarrow$ `bool`) qui retourne $\neg a \land \neg b$.

- Puis écrire une fonction `test_tauto(fct_1,fct_2)` (de signature `test_tauto(fonction,fonction)`$\rightarrow$ `bool`) qui teste si l'équivalence matérielle (correspondant à l'opérateur Python `==`) entre deux fonctions logiques (à deux entrées chacune) $\text{fct}_1(a,b)\leftrightarrow \text{fct}_2(a,b)$  est une tautologie (cela revient à déterminer si les deux fonctions sont d'accord dans tous les cas possibles, donc si leurs tables de vérité sont les mêmes).  
La fonction `test_tauto` prouve donc l'équivalence logique entre les deux fonctions logiques&nbsp;:&nbsp;$\text{fct}_1\equiv \text{fct}_2$

- Prouvez alors la **premiere loi de De Morgan** : $\neg(a\lor b)\equiv \neg a\land\neg b$.

Petit cours sur l'algèbre booléenne dans [cette vidéo](https://www.youtube.com/watch?v=_9nogCrIrIY).

&nbsp;



<br>

---

<br>

## Exercice 5

De nombreuses données scientifiques se présentent sous forme de tableaux ; une façon simple de les transmettre est de les représenter par un **fichier CSV** (pour comma-separated value)&nbsp;: 
il s’agit d’un simple fichier texte, chaque ligne de texte correspondant à une ligne du tableau et un caractère spécial (virgule ou point-virgule le plus souvent) aux séparations entre les colonnes.<br>

Le fichier <a href="pour_TP5/meteo.csv" download="meteo.csv">meteo.csv</a> donne le cumul des précipitations (en mm) et l'ensoleillement (en h) pour différentes villes pour l'année 2018.<br>Écrire dans `exo_5.py` un programme qui récupère les données et affiche les villes de la plus pluvieuse à la moins pluvieuse puis les villes de la plus ensoleillée à la moins ensoleillée.<br>Attention, le séparateur décimal de ces données n'est pas le point anglo-saxon (utilisé par Python) mais la virgule. 
Il faudra les remplacer par des points grâce à la méthode de chaine de caractères `.replace('ancien','nouveau')`. <br>Le séparateur de colonne est, lui, le point-virgule.

&nbsp;



## Exercice 6

Compléter le programme `exo_6.py` pour que le fichier texte créé ( `samedi_censure.txt`) soit une copie censurée du texte dans <a href="pour_TP5/samedi.txt" download="samedi.txt">samedi.txt</a> ; les noms propres "Françoise", "Mirougrain", "Eulalie", "Octave" et "Legrandin" devront être remplacés par des astérisques.<br>Ajouter ensuite le texte censuré `samedi_censure.txt` au repository.

&nbsp;



## Exercice 7

En utilisant la librairie PIL, créer un programme (`exo_7.py`) qui importe l'image <a href="pour_TP5/ascii.jpg" download="ascii.jpg">ascii.jpg</a> et la convertit en "ASCII art" en imprimant à l'écran des caractères différents en fonction de la valeur de l'intensité moyenne d'un pixel.



![](/leonce.png)





## Exercice 8

Modifier le fichier `exo_8.py` pour qu'il affiche le graphique des patients en réa pour toute la France lorsque l'utilisateur tape `0` lors du choix du département. 