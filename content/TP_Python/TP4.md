---
title : "TP4 : Structures de contrôle"
chapter : false
weight : 3
---



# TP4 : Structures de contrôle

*Lien vers le repository GitHub du TP : https://classroom.github.com/a/_smX5cgY*



## Exercice 0

Compléter le programme `exo_0.py` pour qu'il ne cesse de demander le nom de l'utilisateur tant que sa réponse ne fait pas partie de la liste de noms autorisés.<br>

&nbsp;



## Exercice 1

Le ROT13 (rotate by 13 places) est un cas particulier du chiffre de César, un algorithme simpliste de **chiffrement** de texte.  
Comme son nom l’indique, il s’agit d’un décalage de 13 caractères de chaque lettre du texte à chiffrer. Son principal aspect pratique est que le codage et le décodage se font exactement de la même manière.

Indications :  

- utiliser la chaîne de caractères 'abcdefghijklmnopqrstuvwxyz'.
- l'opérateur `in` ou la méthode `isalpha` permettront de savoir si un caractère est alphabétique.
- transformer le caractère (l'opérateur `%` peut s'avérer utile).
- les caractères accentués et les majuscules n'ont pas été modifiés.

Écrire un programme (dans `exo_1.py`) permettant de décoder l'énoncé de l'exercice 2.

&nbsp;



## Exercice 2

Épever ha cebtenzzr dhv genafsbezr ha grkgr qr znavèer à pr dhr yn cerzvèer rg yn qreavèer yrgger qr pundhr zbg erfgr vapunatér nybef dhr yrf yrggerf qr zvyvrh fbag zéynatérf nh unfneq. Ln cbapghngvba qbvg erfgre ra cynpr. Oa cbheen hgvyvfre yn sbapgvba enaqbz.fuhssyr() qh cnpxntr enaqbz dhv zéynatr yrf qvsséeragf éyézragf dh'ba yhv qbaar ra nethzrag.

Texte à modifier (voir `exo_2.py`) : 

> On avale à pleine gorgée le mensonge qui nous flatte, et on boit goutte à goutte une vérité qui nous est amère.

On pourra utiliser la fonction `random.shuffle()` du package random qui mélange les différents éléments qu'on lui donne en argument en se rappelant que les chaînes de caractères sont immuables, il faut donc les transformer en listes (grâce à `list(chaîne)`) si on veut les modifier.

&nbsp;



## Exercice 3

Les alcanes linéaires sont les hydrocarbures de formule brute $\text{C}_n\text{H}_{2n+2}$ dont les carbones forment une chaîne linéaire.  
Écrire (dans `exo_3.py`) un programme donnant la formule semi-développée d'un tel alcane à partir d'une formule brute.  
Par exemple : si `brut = 'C4H10'` alors le programme doit afficher `CH3-CH2-CH2-CH3`. 

&nbsp;



## Exercice 4

L'algorithme de Luhn est une formule de **somme de contrôle** permettant de valider un numéro de carte bancaire.  
On considère le numéro de carte comme une suite de nombres à 1 chiffre.

1. Renverser la liste.
2. Prendre tous les chiffres en position paire dans la liste renversée (2e chiffre, 4e chiffre, etc.) et doubler leur valeur,   
   si le résultat dépasse 10, on ajoute les deux chiffres du résultat (par exemple $6\rightarrow 12 \rightarrow 3$).
3. Sommer tous les nombres de la nouvelle liste (les modifiés et les non-modifiés)
4. Si cette somme vaut 0 modulo 10. Le numéro de carte est valide.

Écrire (dans `exo_4.py`) un programme permettant de vérifier un numéro de carte.

![](/cb.jpg)



## Exercice 5

Que fait ce programme et comment ? (Écrire votre réponse dans `exo_5.md`)


```python
nmax = 5
x = [1]
for n in range(1, nmax+2) :
    print(x)
    x = [([0]+x)[i] + (x+[0])[i] for i in range(n+1)]
```

&nbsp;



## Exercice 6

Dans la série "The Wire", les dealers codent les numéros de téléphone en utilisant une méthode ("jump the five") qui repose sur la disposition des touches sur le clavier.

Chaque numéro (sauf le 5 et le 0) permute avec celui qui se trouve de l'autre côté du 5. <br>Le 5 et le 0 sont intervertis.

Écrire (dans `exo_6.py`) un programme qui crypte et décrypte les numéros de téléphone.

Crypter le numéro de Vieljeux : "05 46 34 79 32‬".

![](/payphone.png?width=400)

## Exercice 7

La **distance de Hamming** entre deux chaînes de caractères de même longueur est le nombre de positions où les caractères sont différents. C'est une notion très importante en théorie du signal puisqu'elle mesure la corruption d'un message transmis.

Écrire (dans `exo_7.py`) un programme pour calculer la distance de Hamming entre deux chaînes.

&nbsp;



## Exercice 8

La suite de Syracuse est une suite d'entiers naturels définie de la manière suivante : <br>on part d'un nombre entier plus grand que zéro ; 

- s’il est pair, on le divise par 2 ; 
- s’il est impair, on le multiplie par 3 et on ajoute 1. 

En répétant l’opération, on obtient une suite d'entiers positifs dont chacun ne dépend que de son prédécesseur.<br>

Lorsque 1 est atteint, un cycle de longueur 3 se répète sans fin : 1, 4, 2, 1, 4, 2, 1,... 

On ajoute donc une nouvelle règle : 

- si 1 est atteint, la suite s'arrête.<br>

1. Construire un programme qui calcule la suite de syracuse du nombre 27 (`exo_8a.py`).
2. Appelons *temps de vol* le nombre de termes de la suite. Modifier le programme pour qu'il donne le temps de vol plutôt que les différents termes (`exo_8b.py`).

La conjecture de Syracuse (ou Collatz) dit que toutes les suites de Syracuse ont une fin.

3. Prouver que la conjecture est vérifiée pour tous les entiers inférieurs à 100 (`exo_8c.py`).

![](/collatz.png)