---
title : "Chaînes de caractères"
chapter : false
weight : 2
pre : "<b>2. </b>"
---

# Les chaînes de caractères



## Définir une chaîne de caractères

Une chaîne de caractères (type `str` pour l'anglais string) est une suite ordonnée de caractères.  
Pour définir une variable de ce type, il suffit d'encadrer des caractères par `'` ou `"` : 


```python
salutation = "Bonjour, monsieur "
```


```python
nom = 'Raoul'
```

Des chaînes de caractères peuvent être **concaténées** (= assemblées) en utilisant l'opérateur `+` :


```python
"abc" + 'def'
```

`'abcdef'`


```python
salutation + nom
```

`'Bonjour, monsieur Raoul'`

On peut aussi utiliser l'opérateur `*` pour répéter plusieurs fois la même chaîne (**dupliquer**) :


```python
'a'*10
```

`'aaaaaaaaaa'`


```python
'-o-'*5
```

`'-o--o--o--o--o-'`

Et on peut combiner `*` et `+` (en utilisant des parenthèses) :


```python
('a' * 4 + 'B') * 3
```

`'aaaaBaaaaBaaaaB'`

&nbsp;

Une chaîne vide est définie simplement comme `''` ou `""`.

Enfin, la fonction `str()` convertit un objet (nombre entier, nombre décimal, liste, etc.) en chaîne de caractères :


```python
str(42)
```

`'42'`


```python
str(3.4e5)
```

`'340000.0'`


```python
str(3.4e20)
```

`'3.4e+20'`

&nbsp;

La fonction native `len()` permet de connaître le nombre de caractère d'une chaîne de caractères (bien noter que les espaces, les fins de ligne ou encore la ponctuation sont aussi des caractères) :


```python
len(salutation)
```

`18`

&nbsp;

&nbsp;



## Caractères d'échappement {#echappement}

Comme on peut utiliser `''` ou `""` pour définir une chaîne, on peut intégrer une citation dans une citation :


```python
'Et il cria : "Mais pourquoi ?"'
```

`'Et il cria : "Mais pourquoi ?"'`

Et pour ajouter encore un niveau de citation, ou pour sauter une ligne, ou pour mettre une apostrophe si notre chaîne est déjà encadrée par des apostrophes, ou pour... ?   
On utilise les **caractères d'échappement**, introduits par un backslash "`\`"&nbsp;!  
Exemples :


```python
phrase = "Et il cria : \"Mais pourquoi ?\""
phrase
```

`'Et il cria : "Mais pourquoi ?"'`


```python
print(phrase)
```

`Et il cria : "Mais pourquoi ?"`

```python
'C\'est donc pour ça...'
```

`"C'est donc pour ça..."`


```python
matières = 'Maths\nPhysique\nAnglais'
matières
```

`'Maths\nPhysique\nAnglais'`


```python
print(matières)
```

`Maths`

`Physique`

`Anglais`


| Caractères d'échappement courants | Signification                     |
| --------------------------------: | :-------------------------------- |
|                              `\'` | apostrophe (')                    |
|                              `\"` | guillemets (")                    |
|                              `\n` | fin de ligne (LF)                 |
|                              `\r` | retour chariot (CR)               |
|                              `\t` | tabulation                        |
|                              `\b` | retour arrière (backspace)        |
|                              `\\` | le caractère backslash            |
|                  `\u`,`\U`,`\N{}` | caractère unicode                 |
|                              `\x` | caractères codés sur un seul byte |

Si vous voulez pouvoir écrire une chaîne de caractères sans qu'un caractère d'échappement n'ait d'effet :


```python
chainebrute = r"Pour une nouvelle ligne, on utilise \n."
chainebrute
```

`'Pour une nouvelle ligne, on utilise \\n.'`


```python
print(chainebrute)
```

`Pour une nouvelle ligne, on utilise \n.`

Cela peut s'avérer pratique pour écrire le chemin d'un fichier sous windows mais écrire des slash à la place (comme sous Unix) est une autre possibilité : 

```python
r'C:\repertoire\fichier.txt'
```

`'C:\\repertoire\\fichier.txt'`


Si on doit utiliser `\n` de manière répétée, le triple guillemet peut nous sauver. Encadré par `'''` ou `"""`, plus besoin de `\n` pour une nouvelle ligne :


```python
a = """un
deux
trois"""
print(a)
```

`un`

`deux`

`trois`

Les strings sont composés de caractères **Unicode** dans Python 3. Unicode est un standard décrivant plus de 100 000 caractères. Chaque caractère se voit assigner un nombre qui est ensuite encodé comme une suite de bytes (qui peuvent être de 8 bits pour le codage UTF-8 le plus répandu et utilisé par Python, de 16 bits, ou de 32 bits).
On a ainsi :


```python
'\u00E9' == '\N{LATIN SMALL LETTER E WITH ACUTE}' == '\xE9'
```

`True`

`\x` permet d'appeler par leur code les 256 premiers caractères (premier byte).


```python
'\x43\x61\x66\xE9'
```

`'Café'`

Cela permet de comprendre ce que Python retourne lorsqu'on entre l'expression suivante :


```python
'prépa ST\b\bTSI'
```

`'prépa ST\x08\x08TSI'`

En effet, le retour arrière `\b` a le code `\x08` (c'est le huitième caractère).


```python
print('prépa ST\b\bTSI')
```

`prépa TSI`

&nbsp;

&nbsp;



## Indexation et slicing

**Indexer** une chaîne permet d'accéder à un caractère individuel de la chaîne. L'indice correspond à la position du caractère. Une chaîne de caractère est un exemple de **séquence** et comme pour toutes les séquences, l'**indice du premier élément est `0`** et l'indice du dernier élément d'une chaîne de n caractères est donc `n-1`.  
Le caractère est retourné dans une chaîne de longueur 1.


```python
a = 'Lycée Vieljeux'
```


```python
a[0]
```

`'L'`


```python
a[6]
```

`'V'`

Les indices positifs comptent dans le sens de la lecture. Mais on peut aussi compter à partir de la fin en utilisant des **indices négatifs** commençant par `-1`.


```python
a[-1]
```

`'x'`


```python
a[-4]
```

`'j'`

Essayer d'indexer en dehors de la chaîne lève une exception `IndexError` qui stoppe l'interprète.


```python
len(a)
```

`14`


```python
a[14]
```

`IndexError: string index out of range`

&nbsp;

Le **slicing** (**découpage**) `s[i:j]` permet d'extraire des éléments de la chaîne ; il extrait une sous-chaîne limitée par les caractères ciblés par les deux indices, incluant l'indice `i` et excluant l'indice `j`.  
Si le premier indice est omis `s[:j]`, il est supposé valoir `0`. Si le deuxième est omis, le slicing s'étend jusqu'à la fin de la chaîne.


```python
a[2:9]
```

`'cée Vie'`


```python
a[:5]
```

`'Lycée'`


```python
a[6:]
```

`'Vieljeux'`


```python
a[:]
```

`'Lycée Vieljeux'`

Ces règles assurent qu'une sous-chaîne est longue de `j-i` caractères (pour des `j` et `i` positifs) et que `s[:i] + s[i:] == s`.  
On peut alors  récupérer une tranche de longueur `r` avec `s[i:i+r]`.


```python
b = 'PrépaTSIdeVieljeux'
```


```python
b[:5]
```

`'Prépa'`


```python
b[5:8]
```

`'TSI'`


```python
b[10:]
```

`'Vieljeux'`

&nbsp;

{{% notice info%}} 

Contrairement à l'indexation, un slicing en dehors des limites ne lève pas d'erreur.  {{% /notice %}}


```python
b[10:20]
```

`'Vieljeux'`

```python
b[20:]
```

`''`

&nbsp;

Un troisième nombre (optionnel) dans un découpage donne un **pas** (qui vaut par défaut `1` s'il est omis) :

```python
b[::2]
```

`'PéaSdVeju'`

```python
b[1::2]
```

`'rpTIeilex'`

```python
b[-1:9:-1]
```

`'xuejleiV'`

Le pas de `-1` dans cette dernière expression correspond à une progression de droite à gauche. Cette découpe commence donc au dernier caractère (`-1` en première position), avance vers la gauche caractère par caractère (`-1` en dernière position) et s'arrête au caractère précédant le `9` dans ce sens, donc le caractère `10`.

**Renverser une chaîne de caractères** devient très simple :

```python
a[::-1]
```

`'xuejleiV eécyL'`

&nbsp;

Pour tester si une chaîne contient une certaine sous-chaîne, on utilise l'opérateur `in` (attention à la casse).


```python
'Vie' in b
```

`True`


```python
'vie' in b
```

`False`

&nbsp;

&nbsp;



## Méthodes liées aux chaînes {#methodeschaines}

Les chaînes sont des objets Python **immuables**,  c.-à-d. qu'on ne peut pas réaffecter un caractère de la chaîne.


```python
a[0] = 'l'
```

`TypeError: 'str' object does not support item assignment`


On peut "augmenter" une chaîne mais cela crée systématiquement une nouvelle chaîne.


```python
a += " de la Rochelle"
print(a)
```

`Lycée Vieljeux de la Rochelle`

```python
b = 'Léonce ' +  a[6:14]
print(b)
```

`Léonce Vieljeux`

&nbsp;

Beaucoup de méthodes permettent de manipuler et transformer les chaînes. On y a accès par la notation point "`.`". Quelques méthodes utiles :

| méthode                        | description                                                  |
| :----------------------------- | :----------------------------------------------------------- |
| `center(longueur,sous-chaîne)` | Complète de part et d'autre la chaîne par la sous-chaîne pour que le résultat ait la taille `longueur`. |
| `endswith(suffixe)`            | Retourne `True` si la chaîne finit par la sous-chaîne `suffixe`. |
| `startwith(préfixe)`           | Retourne `True` si la chaîne commence par la sous-chaîne `préfixe`. |
| `index(sous-chaîne)`           | Retourne l'indice de début de la  `sous-chaîne` dans le chaîne. |
| `strip(cars)`                  | Retourne une copie de la chaîne où les éventuels caractères précisés par *cars* en début ou fin de chaîne sont retirés. Si `cars` est omis, ce sont les espaces éventuels qui sont retirés. |
| `upper()`                      | Retourne une copie de la chaîne avec tous les caractères en majuscule. |
| `lower()`                      | Retourne une copie de la chaîne avec tous les caractères en minuscule. |
| `title()`                      | Retourne une copie de la chaîne  où tous les mots commencent par une capitale et les autres caractères sont en minuscule. |
| `replace(old,new)`             | Retourne une copie de la chaîne où chaque sous-chaîne `old` est remplacée par la sous-chaîne `new`. |
| `split(sep)`                   | Retourne une liste de sous-chaînes obtenues par découpe de la chaîne à chaque séparateur `sep`. Si `sep` n'est pas précisé, la découpe se fait sur les espaces. |
| `join([list])`                 | Utilise la chaîne comme un séparateur pour joindre les différentes chaînes inclues dans la liste. |
| `isalpha()`                    | Retourne `True` si tous les caractères de la chaîne sont alphabétiques. |
| `isdigit()`                    | Retourne `True` si tous les caractères de la chaîne sont des chiffres. |

&nbsp;

Comme ces méthodes retournent toutes une nouvelle chaîne, on peut les enchaîner.


```python
c = '--Prépa TSI du lycée Léonce Vieljeux'
c.strip('--').upper().replace('LÉONCE ','').center(51,'-')
```

`'------------PRÉPA TSI DU LYCÉE VIELJEUX------------'`

&nbsp;

Autres exemples d'utilisation des méthodes :


```python
d = 'java python c++ fortran'
d.isalpha()
```

`False`


```python
e = d.title()
e
```

`'Java Python C++ Fortran'`


```python
f = e.replace(' ',' !\n') + ' !'
f
```

`'Java !\nPython !\nC++ !\nFortran !'`


```python
print(f)
```

`Java !`

`Python !`

`C++ !`

`Fortran !`

```python
f.index('Python')
```

`7`


```python
f[7:].startswith('Py')  # "\n" est compté comme un caractère unique. 
```

`True`


```python
f[7:13].isalpha()
```

`True`

```python
g = d.split(' ')
g
```

`['java', 'python', 'c++', 'fortran']`

```python
h = ' !\n'.join(g)
print(h, end = ' !')
```

`java !`

`python !`

`c++ !`

`fortran !`

&nbsp;

&nbsp;



## La fonction `print`

La fonction native `print()` prend en argument une liste d'objet et, de manière optionnelle, des arguments `end` et `sep` qui spécifient comment doit terminer la chaîne et quels caractères utiliser pour séparer les objets imprimés. 


```python
nom, jour, mois = 'Darwin', 12, 'février'
print(nom,'est né le',jour,mois,1809)
```

`Darwin est né le 12 février 1809`

```python
print('C\'est','tout','collé',sep = '',end = ' !!!\n')
```

`C'esttoutcollé !!!`

```python
print('a')
print('b')
print()
print('c')
```

`a`

`b`

&nbsp;

`c`


Sans argument, `print` imprime le caractère de fin de ligne `\n` car c'est la valeur de l'argument `end` par défaut. Donc pour empêcher la fin de ligne après chaque appel de `print`, il faut donner une autre valeur à `end` comme `end = ''`.


```python
print('Pas de nouvelle ligne.',end = ' ')
print('La preuve !')
```

`Pas de nouvelle ligne. La preuve !`


Avec un peu de pratique, on peut même utiliser `print` pour fabriquer des tableaux de texte :


```python
entête = '| Indice des prix des tulipes |'
ligne = '+' + '-'*16 + '-'*13 + '+'
print(ligne, entête, ligne,
'|  23 févr. 1636 |        100 |',
'|  25  nov. 1636 |        673 |',
'|   1 févr. 1637 |       1366 |', ligne, sep='\n')
```

    +-----------------------------+
    | Indice des prix des tulipes |
    +-----------------------------+
    |  23 févr. 1636 |        100 |
    |  25  nov. 1636 |        673 |
    |   1 févr. 1637 |       1366 |
    +-----------------------------+



&nbsp;

&nbsp;



## Formatage des chaînes de caractères {#formatage}

Grâce à la méthode de chaînes de caractères `.format()`, la chaîne peut contenir la valeur d'une variable.  
La syntaxe la plus simple est :


```python
'{} plus {} égale {}'.format(2,3,'cinq')
```

`'2 plus 3 égale cinq'`

Les arguments de la méthode `str.format()` sont insérés à la place des accolades "`{}`" dans la chaîne principale `str`.  
Un nombre entre accolades se réfère à la position de l'objet passé à la méthode (on peut aussi utiliser des noms s'ils ont été affectés). Cela permet d'utiliser plusieurs fois le même argument.  
Rq : la zone entre les accolades s'appelle champ de formatage.


```python
'{1} plus {0} égale {2}'.format(2,3,'cinq')
```

`'3 plus 2 égale cinq'`


```python
'{0} plus {0} égale {1}'.format(2,2+2)
```

`'2 plus 2 égale 4'`


```python
'{nb1} plus {nb2} égale {rés}'.format(nb1 = 2,nb2 = 3,rés = 'cinq')
```

`'2 plus 3 égale cinq'`

&nbsp;

On peut aussi spécifier une taille minimale à la chaîne qui sera insérée. Si la chaîne passée à la méthode est plus petite que la taille indiquée, elle est complétée par des espaces. La valeur de cette taille souhaitée est placée après un signe "`:`" dans l'accolade. La chaîne insérée est naturellement justifiée à gauche, comportement modifiable grâce à l'ajout de "`>`" ou "`^`". 


```python
'==={0:12}==='.format('Python')
```

`'===Python      ==='`


```python
'==={0:>12}==='.format('Python')
```

`'===      Python==='`


```python
'==={0:^12}==='.format('Python')
```

`'===   Python   ==='`


```python
'==={0:2}==='.format('Python') # Si la taille de la chaîne insérée dépasse la taille allouée, pas de problème...
```

`'===Python==='`

&nbsp;

Cette méthode est aussi utile pour **formater les nombres** qui seront affichés.  
Une lettre ajoutée dans l'accolade spécifie le système de numération : `d` pour la base 10, `b` pour les binaires, `x` ou `X` pour les hexadécimaux (en minuscules ou majuscules).


```python
a = 254
print('a = {0:d} en base 10'.format(a))
print('a = {0:b} en binaire'.format(a))
print('a = {0:x} en héxadécimal (minuscules)'.format(a))
print('a = {0:X} en héxadécimal (majuscules)'.format(a))
```

    a = 254 en base 10
    a = 11111110 en binaire
    a = fe en héxadécimal (minuscules)
    a = FE en héxadécimal (majuscules)


Si on veut que tous les nombres affichés ait la même taille (pour les aligner, par exemple), on peut ajouter des zéros à gauche pour compléter.


```python
'a = {a:05d}'.format(a = 254)
```

`'a = 00254'`

Par défaut, seul le signe d'un nombre négatif est affiché. C'est là encore customisable en ajoutant un signe avant la valeur de la longueur minimum : `'+'` affiche toujours le signe
et `''` ajoute un espace devant si le nombre est positif.


```python
a , b = -25 , 12
s = '{0:+5d}\n{1:+5d}\n= {2:+3d}'.format(a,b,a + b)
print(s)
```

      -25
      +12
    = -13


Les `floats` aussi ont leurs formats propres. Ajouter "`e`" ou "`E`" en fin d'accolade impose un affichage en notation scientifique alors que "`f`" impose l'écriture décimale. Et placer "`.p`" (où `p` est un nombre) après le signe "`:`" précise le nombre `p` de décimales que l'on souhaite (la précision).


```python
a = 1.6235e-6
```

`1.6235e-06`


```python
print('{0:.1e}'.format(a), end = '   ')
print('{0:.8E}'.format(a), end = '   ')
print('{0:.8f}'.format(a), end = '   ')
print('{0:.5f}'.format(a)) # Attention à ne pas tout tronquer !
```

`1.6e-06   1.62350000E-06   0.00000162   0.00000`