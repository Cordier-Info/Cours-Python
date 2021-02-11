---
title : "Fonctions"
chapter : false
weight : 5
pre : "<b>5. </b>"
---

# Fonctions

Une fonction consiste en un bloc d'instructions qui peut être appelé et exécuté à différents endroits et à plusieurs reprises dans le programme.  
Deux avantages à l'utilisation de fonctions :

- elles permettent de réutiliser du code sans avoir à le réécrire,
- elles permettent de décomposer un problème complexe en différentes procédures plus simples, chacune prise en charge par sa propre fonction.

Le code est rendu plus clair et plus facile à débuguer.

&nbsp;

&nbsp;



## Définir et appeler une fonction

L'instruction `def` initialise la définition d'une fonction en lui donnant un nom et des arguments, s'il y en a, que la fonction s'attendra à recevoir lorsqu'elle sera appelée.

Les instructions de la fonction sont écrites dans un bloc indenté qui suit le `def`.

Si à un point quelconque de l'exécution du bloc, une instruction `return` est rencontrée, la valeur spécifiée est renvoyée.  

Par exemple :


```python
def carré(x) :
    x_carré = x**2
    return x_carré
nombre = 2
nombre_au_carré = carré(nombre)
print(nombre,'au carré vaut',nombre_au_carré)
print('8 au carré vaut',carré(8))
```

`2 au carré vaut 4`

`8 au carré vaut 64`



Pour que la fonction renvoie plus d'une valeur, on les emballe dans un tuple.

Exemple : le programme suivant donne les racines d'un trinôme du second degré.


```python
import math
def racines(a,b,c) :
    d = b**2 - 4*a*c
    r1 = (-b - math.sqrt(d))/2/a
    r2 = (-b + math.sqrt(d))/2/a
    return r1, r2

print(racines(1.,-1.,-6.))
```

`(-2.0, 3.0)`

{{%notice note%}}
Une fonction n'est pas obligée de renvoyer explicitement un objet. Si la fin du code est atteinte sans rencontrer un `return`, la valeur spéciale `None` est renvoyée.
{{%/ notice%}}

{{%notice info%}}
La définition d'une fonction peut être écrite n'importe où dans un programme mais une fonction ne peut pas être appelée avant sa définition.
{{%/ notice%}}

{{%notice info%}}
Les fonctions peuvent aussi être **imbriquées** mais une fonction définie à l'intérieur d'une autre fonction ne peut pas être appelée à l'extérieur de cette fonction.
{{%/ notice%}}

&nbsp;

&nbsp;



## Chaîne de documentation

La première ligne du bloc d'une fonction peut servir à la documenter par une chaîne de caractères.

Pour cette chaîne, appelée `docstring`, il est recommandé d'utiliser le triple guillemet qui permet d'écrire simplement sur plusieurs lignes.

Exemple :


```python
def racines(a,b,c) :
    """Retourne les racines de ax^2 + bx + c."""
    d = b**2 - 4*a*c
    r1 = (-b - math.sqrt(d))/2/a
    r2 = (-b + math.sqrt(d))/2/a
    return r1, r2
```

Ce `docstring` devient alors un attribut spécial de la fonction accessible par `__doc__`.


```python
racines.__doc__
```

`'Retourne les racines de ax^2 + bx + c.'`

Une chaîne de documentation devrait expliquer comment utiliser la fonction (quels arguments lui donner et quels objets elle retourne) mais pas détailler son implémentation.



On peut à tout moment renommer une fonction :


```python
rac = racines
rac.__doc__
```

`'Retourne les racines de ax^2 + bx + c.'`

&nbsp;

&nbsp;



## Argument nommé

Dans l'exemple précédent, les arguments sont passés à la fonction dans l'ordre dans lequel ils apparaissent dans la définition. 
Si on veut pouvoir les passer dans un ordre arbitraire, on nomme explicitement les arguments :


```python
racines(a=1., c=-6., b =-1.)
```

`(-2.0, 3.0)`


```python
racines(b=-1., c=-6., a =1)
```

`(-2.0, 3.0)`

&nbsp;

&nbsp;



## Valeur par défaut des arguments

On peut aussi donner à une fonction un **argument 'optionnel'** : si l'appel de la fonction ne précise pas l'argument, une valeur par défaut est fournie.


```python
def exprime_longueur(mesure, unité='m') :
    return 'La longueur vaut {:.2f} {}'.format(mesure,unité)
exprime_longueur(32.831,'cm')
```

`'La longueur vaut 32.83 cm'`


```python
exprime_longueur(10.1)
```

`'La longueur vaut 10.10 m'`

Attention, les arguments par défaut sont affectés dès que l'interprète rencontre la définition pour la première fois. Cela peut amener à des résultats inattendus, en particulier avec des objets muables. <br>Exemple :


```python
def fonc(une_liste = []) :
    une_liste.append(7)
    return une_liste
print(fonc())
print(fonc())
print(fonc())
```

`[7]`

`[7, 7]`

`[7, 7, 7]`



Comme une variable prenant la valeur d'un argument par défaut est affectée au moment de la définition, changer l'affectation de la variable ensuite est sans effet sur l'argument par défaut.


```python
unité_par_défaut = 'm'
def exprime_longueur(mesure, unité = unité_par_défaut) :
    return 'La longueur vaut {:.2f} {}'.format(mesure,unité)
exprime_longueur(10.1)
```

`'La longueur vaut 10.10 m'`


```python
unité_par_défaut = 'année lumière'
exprime_longueur(10.1)
```

`'La longueur vaut 10.10 m'`

&nbsp;

&nbsp;



## Portée des variables

{{% notice info%}}
Une fonction peut définir et utiliser ses propres variables. Ces variables sont alors dites **locales**.   
À l'inverse, les variables affectées en dehors du bloc d'une fonction peuvent être utilisées partout et sont dites **globales**.
{{%/notice%}}

Exemple :


```python
def fct() :
    a = 5
    print(a,b)
b = 6
fct()
```

`5 6`


Comme `b` n'est pas définie dans la bloc de la fonction, Python va la chercher dans le champ global. Mais il faut que `b` soit affectée avant l'appel de la fonction.

Que se passe-t-il si une fonction définit une variable locale avec le même nom qu'une variable globale ?

Le champ local est scruté en premier.

Exemple :


```python
def fct() :
    a = 5
    print(a)
a = 6
fct()
print(a)
```

`5`

`6`


Notons bien que la variable locale `a` n'existe que dans le bloc de définition, qu'elle ait ou non le même nom qu'une variable globale ne change rien. 
Elle disparait quand l'interprète sort de la fonction et n'écrase donc pas la variable globale `a`.

Dans l'ordre, Python regarde d'abord le champ *local*, puis *non local* (le champ englobant la fonction intérieure dans le cas de fonctions imbriquées), 
puis *global*, puis *built-in* (les fonctions natives qu'il convient donc de ne pas redéfinir).

{{% notice note%}}
Une fonction ne peut pas modifier une variable globale sans préciser qu'elle le souhaite.
{{%/notice%}}

Exemple :


```python
x = 2
def fct1() :
    print(x)

def fct2() :
    x += 1
    print(x)
```


```python
fct1()   # pas de problème
```

`2`

```python
fct2()   # aïe
```

`UnboundLocalError: local variable 'x' referenced before assignment`


Pour régler le problème, il faut utiliser le mot clé `global` pour réaffecter la variable globale dans la fonction.


```python
def fct2() :
    global x
    x += 1
    print(x)

fct2()
```

`3`

{{% notice warning%}}
Ce type de réaffectation est néanmoins à éviter, car il amène pas mal de confusion. C'est souvent plus logique de passer `x` en argument de la fonction.
{{%/notice%}}


------

Illsutration avec des listes de parts de pizza :

Il peut être intéressant d'utiliser une fonction pour construire une liste des différents termes d'une **suite définie par récurrence** :

"*The lazy caterer sequence*" (la suite du traiteur paresseux en français) est une suite 
donnant le nombre maximum de morceaux de pizza pouvant être obtenus avec un certain nombre de coupes droites.

Il est simple de voir que $f(0)=1$, $f(1)=2$ et $f(2)=4$.

Et on peut déterminer la relation de récurrence suivante :

$f(n)=f(n-1)+n$

Pour afficher les différents éléments consécutifs de la suite dans une même liste :

```python
def f(suite) :
    suite.append(suite[n-1]+n)
suite = [1]
for n in range(1,16) :
    f(suite) # n et suite sont définis dans le champ global
print(suite)
```

`[1, 2, 4, 7, 11, 16, 22, 29, 37, 46, 56, 67, 79, 92, 106, 121]`

&nbsp;

&nbsp;



## Fonctions lambda : des fonctions anonymes

Avec le mot-clé `lambda`, vous pouvez créer de petites fonctions anonymes très pratiques pour définir des fonctions mathématiques.  
Ces fonctions ne doivent contenir que des expressions. Ainsi, les instructions conditionnelles ou les boucles ou même un `print` sont interdits.  

Exemple :

```python
f = lambda x : x**2 - 3*x + 2

print(f(4.))
```

`6.0`

On peut passer plus d'un argument à une fonction `lambda` grâce à un tuple&nbsp;:

```python
f = lambda x,y : x**2 + 2*x*y + y**2
f(2.,3.)
```

`25.0`

L'explication du terme "fonction anonyme" prend son sens avec l'utilisation de listes de fonctions.  

Exemple de construction d'une liste de fonctions sans utiliser `lambda`&nbsp;:

```python
def const(x) :
    return 1.
def lin(x) :
    return x
def carré(x) :
    return x**2
def cube(x) :
    return x**3
fliste = [const,lin,carré,cube]
fliste[3](5)
```

`125`

`fliste[3]` correspond à la fonction cube et on lui passe l'argument `5`.  

On peut aller plus vite avec les fonctions `lambda` (ici réellement anonymes)&nbsp;:

```python
fliste = [lambda x : 1,
          lambda x : x,
          lambda x : x**2,
          lambda x : x**3]
fliste[3](5)
```

`125`

Les fonctions `lambda` peuvent aussi se montrer pratiques lorsqu'on les associe avec la fonction native `sorted()`.  
En effet, `sorted(liste, key = fonction)` peut prendre en argument une fonction via le mot clé `key`. Cette fonction agit alors sur chaque élément de la liste à trier et `sorted()` trie la liste en fonction du résulat.  

Exemple :

```python
halogènes = [('At',85),('Br',35),('Cl',17),('F',9),('I',53)]
```

Si on veut trier cette liste de tuples contenant le symbole d'un élément halogène et son numéro atomique par numéro atomique croissant on peut utiliser une fonction `lambda` dont le rôle est de récupérer le 2e élément de chaque tuple (= chaque élément de la liste) :

```python
sorted(halogènes, key = lambda e : e[1])
```

`[('F', 9), ('Cl', 17), ('Br', 35), ('I', 53), ('At', 85)]`

&nbsp;

&nbsp;



## Les assertions

Les assertions sont un moyen simple de s'assurer, avant de continuer, qu'une condition est respectée.   

On utilise la syntaxe : `assert test`. Si le test renvoie `True`, l'exécution se poursuit normalement. Sinon, une exception `AssertionError` est levée.  On peut utiliser les assertions pour s'assurer que les arguments d'une fonction vont permettre son exécution.

On peut par exemple reprendre la définition de la fonction `racines` pour s'assurer que les arguments passés sont bien des nombres (et renvoyer un message explicatif si ce n'est pas le cas)&nbsp;:

```python
def racines(a,b,c) :
    """Retourne les racines de ax^2 + bx + c."""
    assert (type(a) is (float or int)) and (type(b) is (float or int)) and (type(c) is (float or int)),\
    	"les arguments de la fonction 'racines' doivent être des nombres !"
    d = b**2 - 4*a*c
    r1 = (-b - math.sqrt(d))/2/a
    r2 = (-b + math.sqrt(d))/2/a
    return r1, r2
```

```
racines(1,6,'-1')
```

`AssertionError: les arguments de la fonction racines doivent être des nombres !`