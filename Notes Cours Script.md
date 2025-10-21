
Langage d'automatisation : 

- Python (pas besoin d'être compilé)
- PowerShell (pas besoin d'être compilé)
- Bash (pas besoin d'être compilé)
- vba
- JavaScript (besoin d'être compilé)
- C (besoin d'être compilé)

## Variables, constantes et types de données

Ce notebook présente les **variables**, **constantes** et **types de données** fondamentaux en Python : chaînes, entiers, flottants, booléens, tuples, dictionnaires, ensembles et listes. Chaque type est accompagné d'exemples pratiques et de démonstrations exécutables.

## Variables et constantes

Une **variable** est un espace mémoire qui stocke une valeur. Elle peut changer au cours du programme.

Une **constante** est une variable que l'on décide de **ne pas modifier** après son initialisation (même si Python ne l'interdit pas techniquement). Par convention, les constantes sont écrites **en majuscules**.


## Les types de données de base

Python gère automatiquement le type des variables (typage dynamique). On peut utiliser la fonction `type()` pour connaître le type d'une variable.


## Les chaînes de caractères (`str`)

Les chaînes permettent de manipuler du texte. On peut les délimiter par des guillemets simples ' ou doubles ". Elles supportent la concaténation, le slicing et diverses méthodes utiles.


## Les nombres entiers (`int`) et réels (`float`)

Les entiers (`int`) représentent des nombres sans décimales, tandis que les flottants (`float`) représentent des nombres à virgule.


## Les booléens (`bool`)

Les valeurs booléennes ne peuvent être que `True` ou `False`. Elles sont souvent le résultat d'une comparaison logique.


## Les tuples (`tuple`)

Un **tuple** est une **collection ordonnée et immuable**. Cela signifie que **l’ordre des éléments est conservé**, mais qu’**on ne peut pas modifier son contenu après sa création** (pas d’ajout, de suppression ou de remplacement d’élément).

Un tuple s’écrit entre **parenthèses `()`**, et ses éléments peuvent être de **types variés** : entiers, chaînes, listes, dictionnaires, etc.

**Caractéristiques principales :**

- Ordonné → on peut accéder aux éléments par leur **index** (`tuple[0]`, `tuple[1]`, …)
- Immuable → on **ne peut pas** changer les éléments une fois le tuple créé
- Peut contenir **des doublons** (contrairement aux `set`)

**Utilité des tuples :**

- Stocker des **valeurs fixes** qui ne doivent pas changer (ex. coordonnées GPS, dimensions, constantes).
- Utiliser comme **clé de dictionnaire** (car immuables).
- Retourner **plusieurs valeurs** depuis une fonction (Python renvoie naturellement un tuple).


## Les listes (`list`)

Une liste est une **collection ordonnée et modifiable**. Elle est très utilisée pour stocker plusieurs valeurs dans un seul objet. Les éléments sont placés entre crochets [].


## Les ensembles (`set`)

Un ensemble est une **collection non ordonnée et sans doublons**. Il est pratique pour les opérations d'ensemble : union, intersection, différence.


## Les dictionnaires (`dict`)

Un dictionnaire stocke des **paires clé-valeur**. Les clés doivent être uniques et servent à accéder rapidement aux valeurs associées.


Un dictionnaire peut contenir **d'autres dictionnaires**. C’est très utile pour représenter des structures de données complexes (par exemple : plusieurs personnes, produits, élèves…).

## Conversion entre types

Python permet de convertir les types avec les fonctions :

- `int()` : pour convertir une donnée en nombre entier
- `float()` : pour convertir une donnée en nombre à virgule flottante
- `str()` : pour convertir une donnée en chaîne de caractères
- `list()` : pour convertir une donnée en une liste
- `tuple()` : pour convertir une donnée (comme une liste par exemple), en tuple
- `set()` : pour convertir une donnée (comme une liste par exemple) en set


## Exercice

nombre1 = int(input("Choisi un nombre "))
nombre2 = int(input("Choisi un deuxième nombre "))
print("Le total de", nombre1, "et",nombre2, "est", nombre1 + nombre2)

