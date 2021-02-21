---
title : "Séquences et itérables"
chapter : false
weight : 3
pre : "<b>3. </b>"
---

# Séquences et itérables



## Séquences

### Listes

Python connaît différents types de données combinées, utilisés pour regrouper plusieurs valeurs. La plus souple est la liste, qui peut être écrite comme une suite, placée entre crochets, de valeurs (éléments) séparées par des virgules. Les éléments d'une liste ne sont pas obligatoirement tous du même type, bien qu'à l'usage ce soit souvent le cas.


```python
liste1 = [1, 'deux', 3.14, 0]
liste1
```

`[1, 'deux', 3.14, 0]`


```python
a = 4
liste2 = [-2.5, a, liste1, a==2, True]
liste2
```

`[-2.5, 4, [1, 'deux', 3.14, 0], False, True]`



Pour créer une liste vide :


```python
liste0 = []
liste0
```

`[]`

&nbsp;

&nbsp;



#### Indexation

{{% notice info%}} 
Comme les chaînes de caractères, **les listes peuvent être indicées et découpées** (slicing) :
{{% /notice %}} 

```python
liste1[1]
```

`'deux'`


```python
liste2[-1]
```

`True`


```python
liste2[2][1]
```

`'deux'`

Ce dernier exemple permet de retrouver le deuxième (indice `1`) élément du troisième (indice `2`) élément de la liste2. Cela marche car il se trouve que `liste2[2]` est une liste et `liste1[1]` est la chaîne de caractère `'deux'`. Et une chaîne de caractère étant elle-même indiçable, on peut écrire :


```python
liste2[2][1][-1]
```

`'x'`


{{% notice info%}} 
On peut utiliser l'opérateur `in` pour tester l'appartenance à une liste :
{{% /notice %}}

```python
1 in liste1
```

`True`


```python
'deux' in liste2
```

`False`


On voit dans ce deuxième exemple que l'opérateur `in` ne regarde pas à l'intérieur des listes contenues dans les listes (on dit qu'il n'agit pas récursivement).  


{{% notice info%}} 
Les listes sont **concaténables** :
{{% /notice %}}

```python
liste1 + liste2
```

`[1, 'deux', 3.14, 0, -2.5, 4, [1, 'deux', 3.14, 0], False, True]`


{{% notice info%}} 
La fonction `len()` permet de connaître la taille d'une liste :  {{% /notice %}}


```python
len(liste1)
```

`4`

`len()` ne compte que les éléments au premier niveau de la liste et non ceux des sous-listes :


```python
len(liste2)
```

`5`

```python
len(liste2[2])
```

`4`



&nbsp;

&nbsp;




#### Slicing

On découpe les listes comme on a découpé les chaînes de caractères :


```python
L = [0., 0.1, 0.2, 0.3, 0.4, 0.5]
L[1:4]
```

`[0.1, 0.2, 0.3]`

On peut obtenir une copie renversée d'une liste en la découpant avec un pas de -1 :


```python
L[::-1]
```

`[0.5, 0.4, 0.3, 0.2, 0.1, 0.0]`

Grâce au pas, on peut aussi sélectionner des éléments périodiquement :


```python
L[1::2]
```

`[0.1, 0.3, 0.5]`



&nbsp;

&nbsp;



#### Mutabilité des listes {#mutabilite}

{{% notice warning%}} 
Contrairement aux chaînes de caractères, les listes sont des objets **mutables**, c'est-à-dire qu'on peut modifier leur contenu.  {{% /notice %}}

On peut ainsi réaffecter des éléments :


```python
L1 = [1, 2, 3]
L1[2] = 'oups'
L1
```

`[1, 2, 'oups']`


```python
L2 = L1
L1[1] = -99
L2
```

`[1, -99, 'oups']`

On remarque que modifier `L1` a modifié `L2`. En effet, `L1` et `L2` référencent la même liste, stockée dans un unique espace mémoire.  

Pour créer une nouvelle liste, copie de la liste de départ, mais indépendante, il y a plusieurs solutions :

```python
L2 = L1.copy()
L3 = L1[:]
L4 = list(L1)
L2[1]=L3[1]=L4[1]='ok'
print(L1,L2,L3,L4)
```

`[1, -99, 'oups'] [1, 'ok', 'oups'] [1, 'ok', 'oups'] [1, 'ok', 'oups']`



Si une liste contient une variable affectée à une certaine valeur et que cette variable est réaffectée, la liste garde l'ancienne valeur car au moment de la définition de la liste, c'est la valeur de la variable et non la variable elle-même qui est stockée en mémoire.


```python
a = 3
L3 = [1, 2, a]
a = 4
L3
```

`[1, 2, 3]`

![](/memoire.png)

Que deviendrait la `liste2` du début après l'instruction `a=2` ?

Des affectations de tranches sont également possibles, ce qui peut  modifier la taille de la liste ou même la vider complètement :


```python
lettres = ['a', 'b', 'c', 'd', 'e', 'f', 'g']
lettres[2:5] = ['C', 'D', 'E']
lettres
```

`['a', 'b', 'C', 'D', 'E', 'f', 'g']`


```python
lettres[2:5] = []
lettres
```

`['a', 'b', 'f', 'g']`


```python
lettres[:] = [] # pour vider entièrement la liste
lettres
```

`[]`

&nbsp;

&nbsp;



#### Méthodes {#methodes}

Le type `list` dispose, comme le type `string`, de méthodes supplémentaires, accessibles avec la notation point "`.`".  
Et comme les listes sont des objets muables, elles peuvent être agrandies ou rétrécies "sur place" (sans avoir à copier le contenu dans un nouvel objet).  
Pour cela, on utilise les méthodes suivantes :  

- `append(x)` : ajoute l'élément `x` à la fin d'une liste.
- `extend(liste_b)` : étend la liste en y ajoutant tous les éléments de la `liste_b`.
- `insert(i,x)`: insère l'élément `x` à la position `i`.
- `remove(x)`: supprime de la liste le premier élément dont la valeur est égale à `x`. Une exception `ValueError` est levée s'il n'existe aucun élément avec cette valeur.


```python
q = []
q.append(4)
q
```

`[4]`


```python
q.extend([6,7,8])
q
```

`[4, 6, 7, 8]`


```python
q.insert(1,5)
q
```

`[4, 5, 6, 7, 8]`


```python
q.remove(7)
q
```

`[4, 5, 6, 8]`



| méthodes utiles | description                                                  |
| :-------------- | :----------------------------------------------------------- |
| `index(x)`      | retourne l'indice de l'élément x (le plus petit s'il est là plusieurs fois) |
| `pop()`         | retire et retourne le dernier élément de la liste            |
| `reverse()`     | inverse l'ordre des éléments (directement dans la liste et non dans une copie comme `liste[::-1]`) |
| `sort()`        | ordonne les éléments dans la liste                           |
| `copy()`        | retourne une copie de la liste (équivaut à `liste[:]`)       |
| `count(x)`      | renvoie le nombre d'éléments ayant la valeur *x* dans la liste |




```python
q.index(8)
```

`3`


```python
q = [2, 0, -1, 3]
```


```python
q.sort()
q
```

`[-1, 0, 2, 3]`



Pour obtenir une copie triée d'une liste sans modifier la liste originale, on peut utiliser la fonction native `sorted()` :


```python
q = ['a', 'e', 'A', 'c', 'b']
sorted(q)
```

`['A', 'a', 'b', 'c', 'e']`


```python
q
```

`['a', 'e', 'A', 'c', 'b']`

On peut aussi utiliser cette fonction pour qu'elle retourne une liste inversée :


```python
sorted(q, reverse=True)
```

`['e', 'c', 'b', 'a', 'A']`



Les méthodes `append()` et `pop()` sont adaptées pour des données structurées en piles (stack en anglais) où le principe est "dernier arrivé, premier sorti" (LIFO pour l'anglais "last in, first out"). Cela sert en particulier pour la gestion de la mémoire. Vous en réentendrez parler.


```python
stack = []
stack.append(1)
stack.append(2)
stack.append(3)
stack.append(4)
print(stack)
```

`[1, 2, 3, 4]`

```python
stack.pop()
```

`4`


```python
print(stack)
```

`[1, 2, 3]`



La méthode des chaînes de caractères `split()` permet de créer une liste à partir d'une chaîne donnée (si non indiqué, le séparateur est l'espace).


```python
mois = 'jan. févr. avr. mai juin'
mois.split()
```

`['jan.', 'févr.', 'avr.', 'mai', 'juin']`


```python
noms = 'Alphonse et Dudule et Raoul et Ursula'
noms.split(' et ')
```

`['Alphonse', 'Dudule', 'Raoul', 'Ursula']`





&nbsp;

&nbsp;



### Tuples

Nous avons vu que les listes et les chaînes de caractères ont beaucoup de propriétés en commun, comme l'indexation et le slicing. Ce sont des exemples de **séquences**. 
{{% notice info%}} 
Les  **séquences** sont une des principales structure de données native en Python. Ce sont des collections **ordonnées** d'objets qui peuvent être **indicées** et **découpées**.{{% /notice %}}

Il existe également un autre type standard de séquence : le tuple.

Un tuple consiste en différentes valeurs séparées par des virgules (avec ou sans parenthèses autour) :


```python
t = 1, 'deux', 3.0, 4
t
```

`(1, 'deux', 3.0, 4)`



Comme un tuple est une séquence, il peut être indexé ou découpé.


```python
t[1]
```

`'deux'`


```python
t[1:3]
```

`('deux', 3.0)`


```python
t[0] = 'essai de réaffectation'
```

`TypeError: 'tuple' object does not support item assignment`

Le dernier exemple montre que les tuples sont des objets immuables.



Pour créer un tuple vide, pas de problèmes : 


```python
t = ()
```

Par contre, c'est plus compliqué de créer un tuple ne contenant qu'un élément (un singleton) :


```python
t = (1,)
```



Si les tuples peuvent sembler similaires aux listes, ils sont généralement utilisés dans des cas et pour des raisons particulières du fait de leur principale différence&nbsp;: 
{{% notice info%}} 
Les tuples sont **immuables** !
{{%/ notice%}} 
Les tuples sont donc utiles lorsqu'une séquence ne peut ou ne devrait pas être modifiée.

On place souvent dans des tuples des collections hétérogènes d'éléments auxquelles on  accèder par "déballage".  
L'instruction `t = 1, 'deux', 3.0` est un exemple d'emballage de tuple : les valeurs `1`, `'deux'`, `3.0` sont "emballées" ensemble.  
On peut ensuite déballer le tuple. Comme on l'a déjà vu, cela permet des affectations multiples.


```python
t = 1, 'deux', 3.0
x , y, z = t
print(x,y,z)
```

`1 deux 3.0`







&nbsp;

&nbsp;



## Objets itérables {#iterables}

{{% notice info%}} 
Les chaînes de caractères, les listes et les tuples sont des exemple d'objets **itérables**&nbsp;: des objets composés d'un ensemble d'éléments  qui peuvent être sélectionnés un par un (=&nbsp;déballés ou unpacked en anglais).  
{{% / notice %}} 

{{% notice note%}} 
Toutes les séquences sont des itérables, mais l'inverse n'est pas vrai (les ensembles (sets), par exemple, sont des itérables mais pas des séquences).
{{% / notice %}} 

L'opérateur `*` permet de **déballer un itérable** (unpack). Cela peut s'avérer pratique lorsqu'une fonction prend en argument plusieurs éléments.  
Prenons l'exemple de la fonction `math.hypot(x,y)` qui calcule $\sqrt{a^2+b^2}$ :


```python
import math
c = [3, 4]
math.hypot(c)
```

`TypeError: hypot expected 2 arguments, got 1`

```python
math.hypot(*c)
```

`5.0`

C'est bien plus simple que d'aller récupérer les éléments de la liste en les indexant (`math.hypot(c[0],c[1])`).



&nbsp;

&nbsp;



### Boucle `for`

C'est souvent utile de récupérer et d'utiliser un à un chacun des éléments d'un objet itérable.  
La syntaxe Python pour une telle opération est plutôt naturelle :  
**for** *élément* **in** *objet itérable* **:**


```python
liste_de_fruits = ['pomme', 'banane', 'orange', 'pamplemousse']
for fruit in liste_de_fruits :
    print(fruit)
```

`pomme`

`banane`

`orange`

`pamplemousse`

Chacun son tour, un élément de l'objet itérable `liste_de_fruits` est affecté à la variable `fruit` dans le block d'instructions qui suit le signe `:`.  
Chaque ligne de ce bloc, le corps de la boucle, doit être indentée par le même nombre d'espaces (c'est recommandé d'utiliser 4 espaces ou une tabulation par niveau d'indentation). C'est cette indentation qui permet, en Python, de savoir qu'on est ou non toujours dans la boucle.  
La structuration du code par indentation est une des principales caractéristiques du langage Python (et un des principaux griefs contre lui).

Une boucle peut très bien être imbriquée dans une autre boucle (il faut indenter le corps de la boucle intérieure d'un niveau de plus) :


```python
for fruit in liste_de_fruits :
    for lettre in fruit :
        print(lettre,end ='.')
    print()
```

`p.o.m.m.e.`

`b.a.n.a.n.e.`

`o.r.a.n.g.e.`

`p.a.m.p.l.e.m.o.u.s.s.e.`

Le `end = '.'` du `print` dans la boucle intérieure permet de placer un point après chaque lettre tout en évitant la nouvelle ligne à chaque appel de la fonction.  
Le `print()` de la boucle extérieure permet d'aller à la ligne à la fin de chaque mot.



&nbsp;

&nbsp;



### `range()`

Si vous devez itérer sur une suite d'entiers, la fonction native `range()` est faite pour cela. Elle génère un objet de type séquence qui permet de créer des suites arithmétiques&nbsp;:


```python
for i in range(5) :
    print(i, end = ' ')
```

`0 1 2 3 4` 


```python
for i in range(1,5) :
    print(i, end = ' ')
```

`1 2 3 4` 


```python
for i in range(0,6,2) :
    print(i, end = ' ')
```

`0 2 4` 


```python
for i in range(10,0,-2) :
    print(i, end = ' ')
```

`10 8 6 4 2` 



`range()` prend donc trois arguments (entier de départ, entier de fin, le pas) dont deux optionnels (range commence à zéro et le pas vaut 1 par défaut).  
Le dernier entier produit par range est celui précédant la valeur de l'entier de fin.



***

**Exemple** : écrire les 20 premiers termes de la suite de Fibonacci définie par $a_1=1$, $a_2=1$ et la relation de récurrence $a_i = a_{i-1}+a_{i-2}$.

*Première méthode : ajouter des éléments à une liste*


```python
n = 20
fib = [1,1]
for i in range(2,n) :
    fib.append(fib[i-1]+fib[i-2])
print(*fib)
```

`1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987 1597 2584 4181 6765`

<div style="page-break-after: always; visibility: hidden"> \pagebreak </div>

*Deuxième méthode (moins consommatrice de mémoire) : on peut se débrouiller pour ne stocker à tout moment que deux éléments.*


```python
n = 20
a, b = 1, 1
print(a, b, end = " ")
for i in range (2,n) :
    a, b = b, a+b
    print(b, end = " ")
```

`1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987 1597 2584 4181 6765` 



&nbsp;

&nbsp;



### `enumerate`

Comme `range()` produit une suite d'entiers, on peut l'utiliser pour afficher l'indice de l'élément d'une liste à chaque itération dans une boucle `for` :


```python
marsupiaux = ['kangooroo' , 'koala' , 'wombat']
for i in range(len(marsupiaux)) :
    print(i, ' : ', marsupiaux[i])
```

`0  :  kangooroo`

`1  :  koala`

`2  :  wombat`


On peut réaliser la même chose plus efficacement en utilisant `enumerate()`.  
Cette fonction prend un objet itérable en argument et produit, pour chaque élément de l'objet, un tuple (*numéro*, *élément*) associant un numéro à l'élément lui-même.


```python
for i, marsupial in enumerate(marsupiaux) :
    print(i, ' : ', marsupial)
```

`0  :  kangooroo`

`1  :  koala`

`2  :  wombat`


Chaque tuple (*numéro*, *élément*) a été déballé dans la boucle `for` en les affectant aux variables `i` et `marsupial`.

On peut faire commencer la numérotation d'`enumerate` à une autre valeur que `0` (mais le numéro ne correspondra alors plus à l'indice). 

```python
for i, marsupial in enumerate(marsupiaux,1) :
    print(i, ' : ', marsupial)
```

`1  :  kangooroo`

`2  :  koala`

`3  :  wombat`



&nbsp;

&nbsp;



### `zip`

Pour faire des boucles sur plusieurs séquences en même temps, on peut utiliser la fonction `zip()` afin d’associer les éléments des différentes séquences entre eux.  
Elle crée un objet itérable composé de tuples couplant les termes de même indice des différentes séquences en argument.


```python
a = [1, 2, 3, 4]
b = ['a', 'b', 'c', 'd', 'e']
for pair in zip(a,b) :
    print(pair)
```

`(1, 'a')`

`(2, 'b')`

`(3, 'c')`

`(4, 'd')`


Ce n'est donc pas grave que les listes n'aient pas la même taille, `zip` les associe tant qu'elle peut.

On peut aussi utiliser `zip` pour dézipper des séquences de tuples :


```python
z = ((1,'a'),(2,'b'),(3,'c'),(4,'d'))
A , B = zip(*z)
print(A, B, sep = '\n')
```

`(1, 2, 3, 4) `

`('a', 'b', 'c', 'd')`

Comme `zip` ne copie pas les éléments vers un nouvel objet, cette méthode est rapide et économe en mémoire ; mais cela signifie aussi qu'on ne peut itérer sur les éléments zippés qu'une seule fois et qu'on ne peut pas les indicer.



&nbsp;

&nbsp;

## Dictionnaires

"dictionnary" est le nom en Python a une structure de données très pratique : la **table de hachage**.  
Un dictionnaire est un contenant, comme une liste ou un tuple, mais au lieu d'indicer les objets s'y trouvant (appelés **valeurs**) par un nombre, on utilise une **clé**.

Une clé peut être n'importe quel objet immuable, mais il s'agit le plus souvent d'une chaîne de caractères.

Exemple où les clés sont des prénoms et les valeurs, des notes :

```python
note = {'Giselle' : 7.5, 'Alphonse' : 12, 'Dudule' : 7.5, 'Berthe' : 16.5}
```

Chaque valeur peut être récupérée grâce à la clé, comme s'il s'agisait d'un indice :

```python
note['Dudule']
```

`7.5`

```python
prenom = 'Berhe'
note[prenom]
```

`16.5`

On peut ajouter une entrée au dictionnaire de la même façon :

```python
note['Raoul'] = 14
note
```

`{'Giselle': 7.5, 'Alphonse': 12, 'Dudule': 7.5, 'Berthe': 16.5, 'Raoul': 14}`

Les dictionnaires sont des objets mutables.

```python
note['Berthe'] = 18
note
```

`{'Giselle': 7.5, 'Alphonse': 12, 'Dudule': 7.5, 'Berthe': 18, 'Raoul': 14}`

Le constructeur `dict()` permet de fabriquer un dictionnaire à partir d'une séquence de paires (*clé*, *valeur*)&nbsp;:

```python
chiffres_romain = dict([(1,'I'),(2,'II'),(3,'III'),(4,'IV'),(5,('V'))])
chiffres_romain[4]
```

`'IV'`

Attention, 4 n'est pas un indice, ici, mais bien une clé.

Si les clés utilisées peuvent constituer des noms de variables, la construction d'un dictionnaire devient encore plus simple&nbsp;:

```python
masse = dict(Mercure = 3.301e23, Vénus = 4.867e24, Terre = 5.972e24)
masse['Terre']
```

`5.972e+24`

{{%notice info%}}

Chaque clé doit être unique, mais les valeurs peuvent être identiques (comme les notes de Dudule et Giselle).

{{%/notice%}}

Tenter d'indicer un dictionnaire par une clé inexistante se solde par une erreur. Pour y échapper, on utilise la méthode `get(clé)`. Un second argument permet de retourner une valeur par défaut en cas d'absence de la clé (sans ce deuxième argument, `get` retournera `None`).

Exemple d'utilisation : fabriquons une liste de 12 éléments pris au hasard parmi les entiers de 1 à 10 et mettons au point une méthode pour compter les occurrences de chacun des 10 entiers&nbsp;:

```python
from random import randint
L = []
for i in range(12) :
    L += [randint(1,10)]
effectifs = dict()
for e in L :
    effectifs[e] = effectifs.get(e,0) + 1
print(effectifs)
```

`{3: 1, 6: 1, 8: 3, 2: 1, 10: 2, 7: 2, 1: 1, 9: 1}`

Les méthodes `keys` et `values` permettents de récupérer les *clés* et *valeurs* d'un dictionnaire sous forme d'itérables, ce qui peut s'avérer pratique pour un tracer, par exemple.

```python
import matplotlib.pyplot as plt
clés = effectifs.keys()
valeurs = effectifs.values()
plt.bar(clés, valeurs)
plt.show()
```

![](/barplot.png?width=800px)

{{%notice note%}}

Les dictionnaires sont des ensemble de paires *clé*-*valeur* qui n'ont aucun ordre particulier. Les dictionnaires ne sont donc pas des séquences.

{{%/notice%}}

&nbsp;

&nbsp;



## Ensembles

Un ensemble (*set* en anglais) est une collection non ordonnée d'objets uniques. Les ensembles sont très pratiques pour retirer des éléments dupliqués d'une séquence et pour déterminer l'union, l'intersection ou la différence entre deux collections.

{{%notice note%}}

Comme ils ne sont pas ordonnées, les ensembles ne peuvent pas être indicés ou découpés. Ce ne sont pas des séquences.

{{%/notice%}}

On crée un ensemble en listant ses éléments à l'intérieur d'accolades `{...}` ou en utilisant le constructeur `set()`&nbsp;:

```python
s = {1,'Coucou !',1,4,3,1,'Coucou !',2,3}
s
```

`{1, 2, 3, 4, 'Coucou !'}`

En transformant la liste `L` de la section précédente (sur les dictionnaires) en ensemble, on peut facilement déterminer le nombre d'éléments dupliqués contenus dans `L` et les éliminer par la même occasion&nbsp;:

```python
S = set(L)
print(S)
nb_duplicata = len(L) - len(S)
print('Nombre de redondances dans L :',nb_duplicata)
```

`{1, 2, 3, 6, 7, 8, 9, 10}`

`Nombre de redondances dans L : 4`



Méthodes s'appliquant aux ensembles&nbsp;:

| Méthode                                                   | Description                                                  |
| --------------------------------------------------------- | ------------------------------------------------------------ |
| `A.isdisjoint(B,...)`                                     | Est-ce que A et B (et autres) sont disjoints ($A \cap B = \emptyset$) ? |
| `A.issubset(B)`  <br />(ou `A <= B`)                      | Est-ce que A est inclus dans B (au sens large) ($A \subseteq B$) ? |
| `A < B`                                                   | Est-ce que A est inclus dans B (au sens strict) ($A \subset B$) ? |
| `A.union(B,...)`  <br />(ou `A | B | ...`)                | Union de A et B (et autres) $A\cup B$                        |
| `A.intersection(B,...)`  <br />(ou `A & B & ...`)         | Intersection de A et B (et autres) $A\cap B$                 |
| `A.difference(B,...)`  <br />(ou `A - B - ...`)           | Différence entre A et B (et autres) $A\backslash B$          |
| `A.symmetric_difference(B,...)`  <br />(ou `A ^ B ^ ...`) | Différence symémtrique entre A et B (et autres) $A\Delta B$  |

Pour illustrer l'utilité des ensembles, voyons comment ils rendent simplissime le passage du crible d'Ératosthène sur les nombres entiers inférieurs à 100 pour y isoler les nombres premiers&nbsp;:

```python
n = 100
P = set(range(2,n)) # ensemble des entiers de 2 à 99
for i in range(2,n//2) :
  M = set(range(2*i,n,i)) # ensemble des multiples de i (autres que i)
  P = P - M  # on retire ces multiples de la liste de départ
print(P) 
```

`{2, 3, 67, 5, 7, 71, 73, 11, 13, 79, 17, 19, 83, 23, 89, 29, 31, 97, 37, 41, 43, 47, 53, 59, 61}`

&nbsp;

&nbsp;

## Listes par compréhension {#comprehension}

La construction de listes par compréhension permet de créer une liste à partir d'un autre objet itérable en une seule ligne de code.  
Par exemple, étant donné une liste de nombres, une liste des carrés de ces nombres peut être créée ainsi :

```python
xliste = [1, 2, 3, 4, 5, 6]
x2liste = [x**2 for x in xliste]
```

La méthode classique prend un peu plus de temps pour s'exécuter et sa syntaxe est plus lourde :

```python
x2liste = []
for x in xliste :
    x2liste.append(x**2)
x2liste
```

`[1, 4, 9, 16, 25, 36]`

Comme on le voit, une construction d'une liste par compréhension est analogue à une définition mathématique.



On peut aussi placer des conditions dans la définition :

```python
[x**2 if x % 2 else x**3 for x in xliste]
```

`[1, 8, 9, 64, 25, 216]`

On a ici mis au carré les nombres impairs et au cube les nombres pairs de `xliste`.



On l'a dit, la construction par compréhension se base sur n'importe quel itérable, pas forcément une liste :


```python
[x**3 for x in range(1,10)]
```

`[1, 8, 27, 64, 125, 216, 343, 512, 729]`

```python
[w.upper() for w in 'abc xyz']
```

`['A', 'B', 'C', ' ', 'X', 'Y', 'Z']`



Enfin, une liste construite par compréhension peut être imbriquée.  
Le code suivant va permettre d'applatir une liste de listes :

```python
vliste = [[1, 2, 3],[4, 5, 6],[7, 8, 9]]
[c for v in vliste for c in v]
```

`[1, 2, 3, 4, 5, 6, 7, 8, 9]`

La première boucle parcourt les différentes listes intérieurs de `vliste` et la deuxième boucle parcourt les éléments de ces listes intérieures. 



***

**Exemple** : supposons que l'on veuille transposer une matrice `M` 3 × 3.

- *Sans compréhension de liste :* 

```python
M = [[1, 2, 3],
     [4, 5, 6],
     [7, 8, 9]]
MT = [[0,0,0],[0,0,0],[0,0,0]]
for i in range(3) :
    for j in range(3) :
        MT[i][j] = M[j][i]
for l in MT :
    print(l)
```

```
[1, 4, 7]
[2, 5, 8]
[3, 6, 9]
```

- *Avec compréhension de liste :*

```python
MT = []
for i in range(3) :
    MT.append([col[i] for col in M])
for l in MT :
    print(l)
```

```
[1, 4, 7]
[2, 5, 8]
[3, 6, 9]
```

Notons toutefois que le package de programmation scientifique NumPy (étudié plus tard) propose une méthode bien meilleure pour gérer les matrices.

***

Les dictionnaires aussi ont droit à leur construction par compréhension. Dans l'exemple suivant, on crée un dictionnaire reportant le nombre de fois que chaque mot apparaît dans un texte.
```python
texte = """texte avec répétitions servant de test pour déterminer le nombre de répétitions de chaque mot dans le texte"""
decompte = {mot: texte.split().count(mot) for mot in set(texte.split())}
decompte
```

`
{'pour': 1,
 'déterminer': 1,
 'avec': 1,
 'servant': 1,
 'texte': 2,
 'le': 2,
 'chaque': 1,
 'test': 1,
 'mot': 1,
 'nombre': 1,
 'répétitions': 2,
 'de': 3,
 'dans': 1}
`

&nbsp;

