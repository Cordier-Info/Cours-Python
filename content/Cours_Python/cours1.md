---
title : "Bases"
chapter : false
weight : 1
pre : "<b>1. </b>"
---

<div>{{ $_hugo_config := { "version": 1 } }}</div>

# Introduction

Python est un langage de programmation interprété développé par Guido van Rossum en 1989. Langage impératif de haut-niveau doté d'une syntaxe simple, Python s'adapte à de nombreux contextes grâce à sa modularité ; une importante librairie de modules et packages permet en effet d'étendre ses capacités.

&nbsp;
&nbsp;

## Shell et IDE

Python possède son propre shell (interface en ligne de commande) : l'utilisateur entre une commande Python qui est interprétée immédiatement lorsque `Entrée` est tapée.  
Au lancement, le shell Python, poli, se présente : 

`Python 3.7.3 (default, Mar 27 2019, 16:54:48)`   
`[Clang 4.0.1 (tags/RELEASE_401/final)] :: Anaconda, Inc. on darwin`  
`Type "help", "copyright", "credits" or "license" for more information.`  
`>>>`

Les 3 chevrons sont l'invite (ou prompt) où les commandes seront écrites.  
IPython, un shell plus évolué, utilise `[1]` comme invite (où le chiffre dans les crochets s'incrémente à chaque commande).  
Pour sortir du shell classique, il faut taper `exit()`, et `exit` ou `quit` pour sortie du shell IPython.

On peut tout à fait exécuter des commandes Python une à une dans le shell.  
Une commande qui renvoie un résultat est appelée **expression**, alors qu'une commande qui ne renvoie rien est une **instruction**.  
Toute fonction est une expression, mais certaines ont en plus un **effet** sur l'environnement comme `print()` qui permet d'afficher une chaîne de caractère dans le shell ou dans un fichier (elle retourne aussi la valeur `None` qui est omise dans ce cas par le shell).


```python
5 + 2
```

`7`


```python
a = 7
```


```python
print(a)
```

`7`

Pour les projets plus complexes nécessitant d'enchaîner les instructions, on écrit l'ensemble de ces commandes (le programme) dans un éditeur de texte et on enregistre le fichier avec une extension `.py`.  
On demande alors à l'interprète Python d'exécuter l'ensemble du script en utilisant la commande `python nom_du_fichier.py` dans le shell de l'OS. Les différents retours dans le shell ne sont alors plus affichés, seuls les effets ont un... effet.  

Le plus simple pour coder est d'utiliser un environnement de travail (**IDE** pour "integrated development environment") qui combine un éditeur de code et un shell Python permettant d'exécuter le script entier ou une partie directement via l'interface. 

{{%notice info%}}

Cela fait parti du bon usage en informatique de **commenter son code** afin qu'il soit plus facilement compréhensible et donc partageable. En Python, les commentaires sont placés derrière un hastag `#` les rendant invisible pour l'interprète.

{{%/notice%}}

```Python
import math  # pour pouvoir utiliser pi (commentaire ignoré par l'interprète)
r = 3  # rayon
2*math.pi*r  # circonférence du cercle de rayon r
```

&nbsp;
&nbsp;

## Installation

L'installation d'[Anaconda](https://www.anaconda.com/products/individual) rend disponible les principales bibliothèques scientifiques Python ainsi que le preformant IDE **Spyder** ou encore **Jupyterlab** (très intéressant pour les présentations de projets car associant dans une même interface texte et code pour former un *notebook*).

[Les oraux de Centrale](https://www.concours-centrale-supelec.fr/CentraleSupelec/SujetsOral/TSI) "Mathématiques 2" et "Physique-chimie 2" utilisent l'IDE [Pyzo](https://pyzo.org). Les ordinateurs du lycée ont les IDE EduPython et Pyzo disponibles sur le serveur `S:\`. Vous pouvez aussi utiliser pour dépanner l'IDE en ligne **Repl.it** depuis le repository du TP.

![](/pyzo.png)


&nbsp;
&nbsp;



## Types de nombres

Les nombres sont parmi les objets Python les plus basiques.  
Il en existe 3 types :

- **les entiers** (type : `int`).  
  Ils n'ont pas de limite de taille (à part la mémoire vive disponible de l'ordinateur).  
  L'arithmétique sur les entiers est exacte.  
- **les nombres à virgule flottante** (type : `float`).  
  Ce sont des nombres décimaux. Ils sont stockés en binaire jusqu'à une certaine précision (l'équivalent de 15 ou 16 chiffres en écriture décimale sur la plupart des systèmes). Ils ne peuvent donc en général pas représenter fidèlement un nombre réel. On reviendra sur ce point plus tard.   
  Rq : c'est un point "." et non une virgule "," qui sépare la partie entière de la partie décimale en Python.
- **les nombres complexes** (type : `complex`).  
  Nombre de type `4+3j` (la partie imaginaire est notée `j` en python).  
  `4+3j` peut aussi s'écrire `complex(4,3)`.



Taper un nombre dans le shell Python renvoie simplement la nombre :


```python
5
```

`5`


```python
5.
```

`5.0`


```python
0.10
```

`0.1`


```python
0.0001
```

`0.0001`


```python
0.0000999
```

`9.99e-05`

Les nombres inférieurs à 0,0001 sont écrits en notation scientifique.




On peut **changer le type d'un nombre**  (conversion) en utilisant les fonctions natives `int()`, `float` et `complex` :


```python
float(5)
```

`5.0`


```python
int(5.2)
```

`5`


```python
int(5.9)
```

`5`

{{% notice note%}} 

On remarque que la transformation en entier d'un nombre décimal prend en fait sa partie entière.  {{% /notice %}}


```python
complex(3.)
```

`(3+0j)`


```python
complex(0.,3.)
```

`3j`



&nbsp;

&nbsp;





## Arithmétique de base {#arithmetique}

Les opérateurs de base utilisables en Python sont :

| symbole | opération                                 |
| :------ | :---------------------------------------- |
| `+`     | addition                                  |
| `-`     | soustraction                              |
| `*`     | multiplication                            |
| `/`     | division décimale                         |
| `//`    | division euclidienne                      |
| `%`     | modulo (reste de la division euclidienne) |
| `**`    | puissance                                 |

Règles de priorités des opérations :  
`**`   >   { `*` ,`/` , `//` , `%` }   >   { `+` ,` -` }


```python
6 / 2 / 4           # comme 3 / 4
```

`0.75`


```python
6 / (2 / 4)         # comme 6 / 0.5
```

`12.0`


```python
2**2**3             # comme 2**(2**3) == 2**8
```

`256`


```python
(2**2)**3          # comme 4**3
```

`64`

Les opérations de priorité égale sont évaluées de gauche à droite à l'exception des puissances (ce qui correspond à évaluer de haut en bas les exposants).  

&nbsp;

&nbsp;





## Méthodes et attributs {#methodes}

En Python, tout, y compris un nombre, est un **objet** ayant certains **attributs** accessibles grâce à la notation "point" : `<objet>.<attribut>`.
Certains attributs sont des simples valeurs : les nombres complexes ont par exemple les attributs `real` et `imag` qui sont les parties réelles et imaginaires d'un nombre complexe.


```python
(3+4j).imag
```

`4.0`



D'autres attributs sont des **méthodes** : des fonctions qui modifient leur objet d'une façon ou d'une autre.  
Par exemple, les nombres complexes ont la méthode `conjugate` qui retourne le complexe conjugué :


```python
(3+4j).conjugate()
```

`(3-4j)`

&nbsp;

&nbsp;





## Fonctions mathématiques {#mathematiques}

`round` et `abs` sont deux fonctions proposées par défaut (natives).  
`abs` retourne la valeur absolue d'un nombre entier ou décimal, ou le module d'un nombre complexe (c'est un exemple de polymorphisme : comportement différent en fonction du type de l'argument).


```python
abs(-7.2)
```

`7.2`


```python
abs(3+4j)
```

`5.0`



`round` arrondi un nombre décimal à l'entier le plus proche (attention, la convention utilisée lorsque la décimale vaut 5 est l'arrondi bancaire ou arrondi au pair le plus proche : au-dessus lorsque la partie entière est impaire et en dessous lorsqu'elle est paire).


```python
round(7.6)
```

`8`


```python
round(7.5)
```

`8`


```python
round(8.5)
```

`8`



Python est un langage d'une grande modularité : des fonctionnalités supplémentaires sont accessibles en important des modules ou des packages qui ne sont pas chargés par défaut (ce qui permet de ne pas encombrer la mémoire).  
Beaucoup de fonctions mathématiques utiles peuvent ainsi être ajoutées grâce au module `math`, importé grâce à la déclaration `import math`.


```python
import math
```


```python
math.exp(-1.5)
```

`0.22313016014842982`


```python
math.cos(0)
```

`1.0`


```python
math.sqrt(9)
```

`3.0`



L'ensemble des fonctions disponibles dans le module sont répertoriées dans sa [documentation en ligne](http://docs.python.org/3/library/math.html) et les plus utiles sont dans le tableau suivant (les angles des fonctions trigonométriques sont supposés en radians) :

| nom de la fonction | signification    | nom de la fonction | signification                        |
| :----------------- | :--------------- | :----------------- | :----------------------------------- |
| `math.sqrt(x)`     | $$\sqrt{x}$$     | `math.atan(x)`     | $$\arctan (x)$$                      |
| `math.exp(x)`      | $$e^x$$          | `math.sinh(x)`     | $$\sinh (x)$$                        |
| `math.log(x)`      | $$\ln (x)$$      | `math.cosh(x)`     | $$\cosh (x)$$                        |
| `math.log(x,b)`    | $$\log_b(x)$$    | `math.tanh(x)`     | $$\tanh (x)$$                        |
| `math.log10(x)`    | $$\log_{10}(x)$$ | `math.asinh(x)`    | $$\text{arsinh} (x)$$                |
| `math.sin(x)`      | $$\sin (x)$$     | `math.acosh(x)`    | $$\text{arcosh} (x)$$                |
| `math.cos(x)`      | $$\cos (x)$$     | `math.atanh(x)`    | $$\text{artanh} (x)$$                |
| `math.tan(x)`      | $$\tan (x)$$     | `math.hypot(x,y)`  | norme euclidienne $$\sqrt{x^2+y^2}$$ |
| `math.asin(x)`     | $$\arcsin (x)$$  | `math.degrees(x)`  | convertit x des radians aux degrés   |
| `math.acos(x)`     | $$\arccos (x)$$  | `math.radians(x)`  | convertit x des degrés aux radians   |

Le module `math` propose aussi deux attributs très utiles : math.pi et math.e qui donnent les valeurs de $\pi$ et $e$.

Il est possible d'importer le module `math` par la commande `from math import *` afin d'accéder à ses fonctions directement :


```python
from math import *
```


```python
cos(pi)
```

`-1.0`

Bien que cela puisse être pratique pour des petites interactions avec le shell, ce n'est pas recommandé pour des programmes plus conséquent car cela peut générer confusions et conflits de noms.

On peut bien sûr composer les fonctions :


```python
math.degrees(math.acos(math.sqrt(3)/2))
```

`30.000000000000004`

Notons que le nombre affiché diffère du résultat exact attendu $\arccos(\sqrt{3}/2)=30°$. C'est dû au codage machine des flottants qui ne permet qu'une précision limité.

&nbsp;

&nbsp;






## Variables

Lorsqu'un objet, comme un `float`, est créé dans un programme Python, une certaine place en mémoire lui est allouée. Cette place est repérée par une adresse dont la valeur peut être obtenue grâce à la fonction `id()`.


```python
id(3.7)
```

`4387417928`



Il est beaucoup plus pratique de pouvoir récupérer une valeur en mémoire grâce à un petit nom plutôt que par son adresse. C'est à ça que servent les variables. Une variable est liée à un objet grâce à une **affectation** et identifie cet objet pour les calculs suivants.  


```python
a = 3
```


```python
b = -0.1
```


```python
a * b
```

`-0.30000000000000004`

À nouveau, le résultat décimal affiché est un peu étrange, toujours à cause de la précision limité des flottants (environ 16 chiffres significatifs seulement)...

Si on veut pouvoir utiliser le résultat de `a * b` pour des calculs ultérieurs, il faut lui aussi le stocker en mémoire.


```python
c = a * b
```


```python
c
```

`-0.30000000000000004`



Contrairement à des langages à typage statique comme le C, **une variable n'a pas besoin d'être déclarée en Python**. On parle alors de **typage dynamique.** Mais il faut néanmoins initialiser la valeur de la variable pour ne pas provoquer d'erreur. Le type de la variable est induit au moment de cette première affectation.

```
3+x
```

`NameError: name 'x' is not defined`

On peut interroger le type d'une variable avec la fonction `type()` :  


```python
type(c)
```

`float`

&nbsp;

Règles sur les noms de variables :

- ils sont sensibles à la casse (minuscule ou majuscule)
- ils peuvent contenir n'importe quelles lettres ou chiffres et le tiret-bas "_" mais ne doivent pas commencer par un chiffre.
- certains noms sont interdits (attention en particulier à lambda) :

`and`  `assert`  `break`  `class`  `continue`  `def`  `del`  `elif`  `else`  `except`  `finally`  `for`  `from`  `global`  `if`  `import`  `in`  `is`  `lambda`  `nonlocal`  `not`  `or`  `pass`  `print`  `raise`  `return`  `try`  `while`  `yield`



{{% notice warning%}} 

Il est important pour la lisibilité de son code de donner les noms les plus explicites possibles aux variables. Les rapports de jury le répète tous les ans... {{% /notice %}}

Rapport 2019 de l'épreuve de Centrale par exemple :

>**Des noms de variables explicites aident à la compréhension du code. De trop nombreux candidats utilisent des noms de variables quelconques (a, b, c...) ce qui nuit à la compréhension du programme. La clarté du programme (en particulier le choix des noms de variables) ainsi que la présence de commentaires opportuns sont prises en compte dans l’évaluation.**



&nbsp;

Une affectation ne retourne rien (c'est une instruction) mais a un effet sur la mémoire : l'adresse de la variable est modifiée à chaque nouvelle affectation. C'est ce qui rend possible les réaffectations à partir de la variable elle-même.


```python
id(a)
```

`4304751488`


```python
id(a+1)
```

`4304751520`


```python
a = a + 1
```


```python
id(a)
```

`4304751520`

Ces types de **réaffectation** sont si fréquents qu'il existe une notation raccourcie : `+=`, `-=`, `*=`, `/=`, `//=`, `%=`.

Ainsi, `a += 1` équivaut à `a = a + 1` et `b /= 5` équivaut à `b = b/5`.

&nbsp;

Python permet d'**affecter plusieurs variables simultanément** (en parallèle) :


```python
a , b = 3.2 , -2
```


```python
a
```

`3.2`


```python
b
```

`-2`

Comment faire si on veut permuter les valeurs auxquelles sont liées deux variables ? Dès qu'on écrit `a = b`, la valeur initiale de `a` est perdue et si on commence par `b = a`, c'est la valeur initiale de `b` qui est perdue. Il faudrait donc utiliser une variable temporaire et écrire : `tmp = a`, `a = b` et `b = tmp`.   
Mais l'affectation parallèle de Python va nous permettre d'être plus élégants. Il suffit en effet d'une petite ligne :


```python
a , b = b , a
```


```python
a
```

`-2`


```python
b
```

`3.2`

L'affectation parallèle repose sur le packing et l'unpacking de tuples, mais on verra ça dans un prochain cours.

&nbsp;

&nbsp;



## Comparaison et logique

Les différents comparateurs utilisables en Python sont :

| comparateur | signification       |
| :---------- | :------------------ |
| `==`        | égal à              |
| `!=`        | différent de        |
| `>`         | supérieur à         |
| `<`         | inférieur à         |
| `>=`        | supérieur ou égal à |
| `<=`        | inférieur ou égal à |

Le résultat d'une comparaison est un objet booléen (type `bool`) qui a deux valeurs possibles : `True` ou `False`. 


```python
7 == 8
```

`False`


```python
4 >= 3.8
```

`True`

```python
a = 4 < 3
type(a)
```

`bool`



Il faut bien noter la différence entre `=` qui affecte une valeur à une variable et `==` qui compare deux valeurs.  

{{% notice warning %}} 

La précision finie des nombres flottants rend leur comparaison dangereuse : {{% /notice %}}


```python
a , b = 0.01 , 0.1**2
```


```python
a == b
```

`False`

En effet :


```python
a
```

`0.01`


```python
b
```

`0.010000000000000002`



Les comparaisons peuvent être modifiées et enchaînées grâce aux opérateurs logiques `and` (et), `or` (ou inclusif), et `not` (non).  


```python
7.0 > 4 and -1 >= 0
```

`False`


```python
5 < 4 or 1 != 0
```

`True`

Dans des expressions composées comme celles-ci, les opérateurs de comparaison sont évalués en premier puis vient le tour des opérateurs logiques.


```python
not 7.5 < 0.9 or 4 == 4
```

`True`


```python
not (7.5 < 0.9 or 4 == 4)
```

`False`



Un nombre entier ou décimal peut être considéré comme un booléen dans des expressions logiques. Dans ce cas, tout nombre différent de zéro est considéré comme vrai.


```python
18.7 and 5 < 8
```

`True`



{{% notice note%}} 

On parle d'**égalité de valeurs** (testée par l'opérateur `==`) lorsque deux variables référencent la même valeur et d'**égalité physique** lorsqu'il s'agit du même objet ayant un emplacement mémoire unique. L'égalité physique implique bien sûr l'égalité de valeurs.   {{% /notice %}}

Pour tester l'égalité physique de deux variables, on utilise l'opérateur `is`. 

```python
a = 257
b = 257
a == b
```

`True`

```python
a is b
```

`False`

```python
a is 257
```

`False`

```python
id(a)
```

`4396188400`

```python
id(b)
```

`4396188144`

```python
id(257)
```

`4396188272`

```python
c = 256
d = 256
c is d
```

`True`

```python
c is 256
```

`True`

```python
id(c)
```

`4304759584`

```python
id(d)
```

`4304759584`

```python
id(256)
```

`4304759584`

Python garde en cache les petits entiers (de -5 à 256 généralement), souvent utilisés, pour améliorer les performances. `a` et `b`
 sont alors tout deux liés à l'espace mémoire de l'objet `256`. Ils correspondent donc bien au même objet physique.

&nbsp;

&nbsp;





## Type `None`

Enfin, pour nous aider à traiter les cas où aucune valeur définie n'est possible (soit parceque la valeur conduirait à une erreur où n'aurait pas de sens), Python propose d'utiliser la valeur `None` de type `NoneType`.  
C'est particulièrement utile pour éviter des valeurs par défaut arbitraireS comme `0` ou `-99` pour des données manquantes ou corrompues.  
On en verra un exemple d'utilisation dans le TP 3.