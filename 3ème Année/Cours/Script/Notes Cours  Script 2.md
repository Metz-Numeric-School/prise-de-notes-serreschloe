
# Les structures conditionnelles

Ce notebook couvre en profondeur les **conditions** en Python : opérateurs de comparaison, booléens, `if / elif / else`, opérateurs logiques, _truthiness_, expressions conditionnelles (ternaires), imbrication, et les pièges fréquents.

## 1. Booléens et opérateurs de comparaison

### Définition

Un booléen (ou valeur booléenne) est un type de donnée logique qui ne peut prendre que deux valeurs possibles :

- 👉 `True` (vrai)
- 👉 `False` (faux)

Ce type sert à exprimer une condition logique, un état ou le résultat d’une comparaison.

**Opérateurs de comparaison courants :**

- `==` égalité
- `!=` différence
- `<`, `<=`, `>`, `>=`
- `in` (appartenance), `not in`

Les comparaisons **retournent un booléen**.

## 2. La structure `if / elif / else`

Syntaxe :

```
if condition_1:    bloc_1elif condition_2:    bloc_2else:    bloc_sinons
```

Notez bien l'utilisation des ":" à la fin des lignes précédent les blocs.

Les blocs, eux, sont déterminés par **l'indentation**. Dès qu'une condition est vraie, son bloc s'exécute et **les autres ne sont pas évaluées**.

Les conditions `elif` et `else` sont optionnelles. Vous pouvez avoir uniquement un `if`.

⚠️ **Attention** : un `elif` ou un `else` ne peuvent pas être utilisés sans `if` !

## 3. Opérateurs logiques : `and`, `or`, `not`

- `A and B` est vrai si **A ET B** sont vrais.
- `A or B` est vrai si **au moins l'un** des deux est vrai.
- `not A` inverse la vérité de `A`.

Ces opérateurs **sont à court-circuit** :

- Avec `and`, si `A` est faux, Python **n'évalue pas** `B`.
- Avec `or`, si `A` est vrai, Python **n'évalue pas** `B`.


## 4. Truthiness (valeurs évaluées comme vrai/faux)


La **truthiness** (ou _valeur de vérité implicite_) désigne la **façon dont Python évalue une valeur comme "vraie" ou "fausse"**, même si ce n'est **pas un booléen explicite** (`True` ou `False`).

Autrement dit, **toute valeur en Python peut être interprétée comme vraie ou fausse** lorsqu'elle est utilisée dans un contexte logique (par exemple dans un `if`).

**Règle générale :**

- ✅ **Valeurs considérées comme vraies ("truthy")** → Presque tout ce qui **n'est pas vide ou nul** : `1`, `"bonjour"`, `[1, 2]`, `{ 'clé': 'valeur' }`, etc.
    
- ❌ **Valeurs considérées comme fausses ("falsy")** → Les valeurs **vides ou nulles** : `0`, `0.0`, `''`, `[]`, `{}`, `set()`, `None`, `False`
    

**🧠 À retenir :**

> La **truthiness** est la capacité de Python à **interpréter automatiquement une valeur comme vraie ou fausse** dans un test logique, sans exiger qu'elle soit explicitement `True` ou `False`.


## 5. Expression conditionnelle (ternaire)

Forme compacte pour affecter une valeur selon une condition :

```
valeur = expression_si_vrai if condition else expression_si_faux
```

À utiliser pour des cas simples (lisibilité avant tout).

## 6. Imbrication vs. chaîne de `elif`

Évitez les imbrications trop profondes. Préférez une **chaîne de `elif`** claire.

## 7. Bonnes pratiques et pièges fréquents

1. **Utiliser == pour comparer des valeurs**.
2. **Attention à l'assignation vs. comparaison** : = assigne, == compare.
3. **Comparer des types compatibles** (éviter 3 < '3').
4. **Lisibilité** : préférez des conditions nommées (variables intermédiaires) si l'expression devient longue.
5. **Chaînage de comparaisons** : Python permet 18 <= age < 65.
6. **Court-circuit** : utile pour éviter des erreurs (ex. vérifier obj non nul avant obj.attr).
7. **Ne pas abuser des ternaires** : au-delà d'un cas simple, préférez if.


## 8. Mise en pratique

### Exercice 1 — Pair / impair

---

Écrire un programme qui lit un entier `n` (déjà fourni) et affiche `pair` si `n` est pair, sinon `impair`.

🧠 **Pour aller plus loin :** vous pouvez aller récupérer le nombre avec une saisie utilisateur (`input()`). N'oubliez pas de vérifier les types.

n = 8  
if n % 2 == 0:
  print("Pair")
else:
  print("Impair")


### Exercice 2 — Tarif réduit

---

On applique un **tarif réduit** si l'utilisateur a **moins de 26 ans** **ou** est **bénéficiaire du RSA**. Sinon, tarif normal. Afficher `reduit` ou `normal`.

age = 78
beneficiaire_rsa = False
if age < 26 or beneficiaire_rsa:
  print("Réduit")
else:
  print("Normal")

### Exercice 3 — Catégorisation de notes

---

À partir d'une `note` sur 20, afficher :

- `<10` : `ajourné`
- `10 à 11.99` : `passable`
- `12 à 13.99` : `assez bien`
- `14 à 15.99` : `bien`
- `>= 16` : `très bien`


note = float(input("Note /"))
if note < 10:
  print("ajourné")
elif note < 12:
  print("passable")
elif note < 14:
  print("assez bien")
elif note < 16:
  print("bien")
elif note >= 16:
  print("tres bien")


### Exercice 4 — Login très simplifié

---

Demandez (via les variables déjà posées) `username` et `password`. Affichez `OK` si les deux correspondent aux références, sinon `KO`.

**Références :** `ref_user = 'admin'`, `ref_pwd = '1234'`

ref_user = 'admin'
ref_pwd = '1234'

username = 'admin'   # simule une saisie
password = '1234'    # simule une saisie

  if username == ref_user and password == ref_pwd:
  print("OK")
else:
  print("KO")


### Exercice 5 — Sécurité accès mineurs

---

Affichez `autorisé` si l'utilisateur a 18 ans **ou plus**, sinon `refusé`. Faites-le en utilisant une expression conditionnelle (**ternaire**)

age = 45

if age >= 18:
  print("autorisé")
else:
  print("refusé")

