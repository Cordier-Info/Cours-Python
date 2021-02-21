---
title : "Structures de contrôle"
chapter : false
weight : 4
pre : "<b>4. </b>"
---

# Structures de contrôle

Python étant un langage impératif, il possède des structures de contrôle permettant de dévier le flot d'exécution. 
Les structures de contrôle travaillent sur des blocs d'instructions contigües qui sont repérés par leur indentation en Python.  

Les deux grandes familles de commandes de blocs sont :

- les alternatives : exécuter un bloc d'instructions si une certaine condition est réunie (*si ... sinon si ... sinon*) ;
- les boucles : exécuter un bloc d'instructions à plusieurs reprises (boucle "*tant que*" et les boucles avec compteur `for` déjà rencontrées).

&nbsp;

&nbsp;



## `if` ... `elif` ... `else`

La structure `if ... elif ... else` permet d'exécuter des instructions seulement si une condition, donnée par le résultat d'un ou plusieurs tests logiques, est vérifiée. 

`if` <*expression logique 1*> :  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<*bloc d'instructions 1*>  
`elif` <*expression logique 2*> :  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<*bloc d'instructions 2*>  
**...**  
`else` :  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<*bloc d'instructions*>

Si l'<*expression&nbsp;logique&nbsp;1*> est évaluée comme vraie, le <*bloc&nbsp;d'instructions&nbsp;1*> est exécuté ; dans le cas contraire, si l'<*expression logique&nbsp;2*> est évaluée comme vraie, le <*bloc&nbsp;d'instructions&nbsp;2*> est exécuté, et ainsi de suite&nbsp;; et si aucune des expressions logiques précédentes n'est vraie, le bloc d'instructions faisant suite au `else:` est exécuté.

Par exemple :


```python
for x in range(10) :
    if x<= 3 :
        print(x,'est inférieur ou égal à 3')
    elif x > 5 :
        print(x,'est plus grand que 5')
    else :
        print(x,'doit être 4 ou 5')
```

    0 est inférieur ou égal à 3
    1 est inférieur ou égal à 3
    2 est inférieur ou égal à 3
    3 est inférieur ou égal à 3
    4 doit être 4 ou 5
    5 doit être 4 ou 5
    6 est plus grand que 5
    7 est plus grand que 5
    8 est plus grand que 5
    9 est plus grand que 5

{{%notice note%}}

Python reconnaît comme vrai n'importe quel type de donnée (même pas besoin d'expression logique) du moment qu'il ne s'agit ni de l'entier `0`, du décimal `0.`, de la chaîne de caractères vide `''`, du tuple vide `()`, de la liste vide `[]`, ou encore de la valeur `None`. 

{{% / notice %}}


```python
for x in range(10) :
    
    if x :                       # vrai pour tout x ≠ 0
        print(', ',end = '')
        
    if x % 2 :                   # vrai pour tout x impair
        print(x,'est impair', end = '')
    else :
        print(x,'est pair', end = '')
        
print('',end = '.')              # pour le point final
```

    0 est pair, 1 est impair, 2 est pair, 3 est impair, 4 est pair, 5 est impair, 6 est pair, 7 est impair, 8 est pair, 9 est impair.



Exemple :  
Dans le calendrier grégorien, une année est bissextile si elle est divisible par 4 sauf si elle est aussi divisible par 100 à part les années divisibles par 400 qui sont bien bissextiles.  
Le programme suivant détermine si une année est bissextile :


```python
année = 2020
if not année % 400 :
    est_bissextile = True
elif not année % 100 :
    est_bissextile = False
elif not année % 4 :
    est_bissextile = True
else :
    est_bissextile = False
s = 'est une' if est_bissextile else "n'est pas une"
print("L'année", année , s ,"année bissextile.")
```

`L'année 2020 est une année bissextile.`



&nbsp;

&nbsp;



## Boucles `while`

Alors qu'une boucle `for` tourne un nombre de fois fixé à l'avance, une boucle `while` exécute son bloc d'instructions tant qu'une certaine condition est validée. 


```python
i = 0
while i < 10 :
    i += 1
    print(i,end ='.')
print('\nLa boucle est finie...')
```

    1.2.3.4.5.6.7.8.9.10.
    La boucle est finie...

Le compteur `i` est initialisé à `0` et comme `0` est inférieur à `10`, la boucle `while` démarre. À chaque itération, `i` est incrémenté de `1` et sa valeur affichée. Puis `i` atteint `10` et à l'itération suivante `i < 10` devient faux, la boucle s'arrête et l'éxécution reprend après la boucle.  
On voit avec cet exemple qu'un équivalent de boucle `for` peut facilement être construit avec une boucle `while`.



Un exemple plus intéressant :  
implémentons l'algorithme d'Euclide permettant de déterminer le plus grand diviseur commun de deux entiers.


```python
a , b = 1920 , 1080
print('pgcd({},{}) = '.format(a,b),end = '')
while b :
    a , b = b, a % b
print(a)
```

`pgcd(1920,1080) = 120`

La boucle continue jusqu'à ce que `b` divise `a`. À chaque itération, `b` prend la valeur du reste de la division euclidienne de `a` par `b` et `a` prend l'ancienne valeur de `b`.  
`while b` est équivalent à `while b != 0` puisque la valeur `0` est évaluée comme fausse.



&nbsp;

&nbsp;



## `break`, `continue` et `else`

Python propose 3 instructions supplémentaires pour contrôler le flux d'un programme.



### `break`

L'instruction `break`, placée dans le bloc d'instructions d'une boucle, met immédiatement fin à cette boucle lorsqu'arrive son tour d'être exécutée.  
L'exécution reprend à l'instruction suivant la boucle.  


```python
x = 0
while True :
    x += 1
    if not (x % 15 or x % 25) :
        break
print(x,'est divisible à la fois par 15 et 25.')
```

`75 est divisible à la fois par 15 et 25.`

La condition du `while` est ici littéralement toujours vraie donc la seule sortie possible de la boucle passe par une exécution de l'instruction `break`, ce qui ne peut arriver que si `x` est à la fois divisible par 15 et 25.



De la même manière, pour trouver l'indice de la première occurrence d'un nombre négatif dans une liste :


```python
liste = [5, 2, 99, 0, 100, -2, 37, 43, -124]
for i, a in enumerate(liste) :
    if a < 0 :
        break
print("L'élément d'indice",i,"valant",a,"est le premier élément négatif.")
```

`L'élément d'indice 5 valant -2 est le premier élément négatif.`

{{%notice note%}}

Après la sortie de la boucle, les variables `i` et `a` gardent les valeurs qu'elles ont au moment de l'instruction `break`. 

{{%/ notice%}}

&nbsp;




### `continue`

`continue` marche comme `break` mais au lieu de sortir de la boucle, l'instruction force immédiatement la prochaine itération de la boucle sans accomplir le reste des instructions du bloc pour l'itération en cours.


```python
for i in range(1,11) :
    if i % 2 :
        continue
    print(i,'est pair')
```

    2 est pair
    4 est pair
    6 est pair
    8 est pair
    10 est pair

Si `i` n'est pas divisible par 2 et donc que `i % 2 = 1`, ce qui est considéré comme `True`, `continue` est appelé et on passe alors directement au `i` suivant, et donc l'instruction `print` est sautée.

&nbsp;




### `else`

On peut faire suivre une boucle `for` ou `while` d'un bloc introduit par une instruction `else`. Ce bloc n'est exécuté que si la boucle se termine "normalement", i.e. sans rencontrer un `break`.  
Pour voir son utilité, reprenons le code repérant la première occurrence d'un nombre négatif.


```python
liste = [5, 2, 99, 0, 100, 2, 37, 43, 124]
for i, a in enumerate(liste) :
    if a < 0 :
        break
print("L'élément d'indice",i,"valant",a,"est le premier élément négatif.")
```

`L'élément d'indice 8 valant 124 est le premier élément négatif.`


On constate que le programme se comporte bizarrement si la liste ne contient que des nombres positifs.  
Un `else` va nous sauver :


```python
liste = [5, 2, 99, 0, 100, 2, 37, 43, 124]
for i, a in enumerate(liste) :
    if a < 0 :
        print("L'élément d'indice",i,"valant",a,"est le premier élément négatif.")
        break
else :
    print("Aucun élément négatif")
```

`Aucun élément négatif`




Autre exemple d'utilisation : une manière peu élégante de déterminer le plus grand diviseur d'un nombre.


```python
a = 2019
b = a - 1
while b != 1 :
    if not a % b :
        print('le plus grand diviseur de',a,'est',b)
        break
    b -= 1
else :
    print(a,'est premier !')
```

`le plus grand diviseur de 2019 est 673`


&nbsp;

&nbsp;



## La gestion des exceptions



Python distingue deux types d'erreurs : 

- les **erreurs de syntaxe** : elles correspondent à des erreurs dans la grammaire du langage et sont toujours fatales. Elles se soldent par un pénible `Syntaxerror : invalid syntax` ou encore un `IndentationError: expected an indented block`. Exemple typique : `if a = 2 :` (au lieu de `if a == 2`).
- les **exceptions** : erreurs non syntaxiques rencontrées pendant l'exécution. Exemples : `ZeroDivisionError`, `NameError`, `TypeError`. Elles nes sont pas forcément fatales si on les gère en amont.

Gestion des exceptions : on peut indiquer à l'interprète quoi faire s'il rencontre une exception lors de l'exécution. Pour cela, on utilise les instructions `try :`  et `except :`.   
Le bloc introduit par `try` correspond à ce qui doit être exécuté en l'absence d'exception, et celui introduit par `except` permet de gérer une exception donnée.  

Prenons l'exemple de la gestion d'une division par zéro :

```python
for i in range(-2,3) :
    y = 1 / i
    print('1 /',i,'=',y)
```

`1 / -2 = -0.5`  
`1 / -1 = -1.0`    ![](/exception.png)

L'exécution a été interrompue... Mais si on utilise `try / except`&nbsp;:

```python
for i in range(-2,3) :
    try :
        y = 1 / i
        print('1 /',i,'=',y)
    except ZeroDivisionError :
        print('1 / 0 : Division par zéro impossible !')
```
`1 / -2 = -0.5`  
`1 / -1 = -1.0`   
`1 / -1 = -1.0`    
`1 / 0 : Division par zéro impossible !`  
`1 / 1 = 1.0`   
`1 / 2 = 0.5`  

L'exécution va à son terme.

Autre exemple classique : gérer les entrées farfelues de l'utilisateur.
```python
while True:
    try :
        x = int(input("Entrez un nombre svp : "))
        break
    except ValueError :
        print("Oops! Pas un nombre valide. Essayez à nouveau... ")
```
On verra un [dernier exemple un peu plus touffu](../cours6/#lire-un-fichier) dans le chapitre 6 sur la manipulation de fichier.

