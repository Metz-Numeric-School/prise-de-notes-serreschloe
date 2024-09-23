## Variables

Nom (pas de caractères spéciaux, pas d'espace, pas commencer par un chiffre) et une Valeur (differents types de valeurs)

Exemple variable : prenom = "john"
= -> affectation, declaration, initialisation
"John" -> chaine de caractères 

ex : NOMS DE VARIABLES

dateJour = "23-09-2024"
anneeNaissance = 1988

## Conventions de nommage

- LowerCamelCase = camelCase - PascalCase
- UpperCamelCase = CamelCase
- snake_case (uniquement à python)
- kebab-case (nom de fichier ou URL) 

année_naissance (non)
birth_year (oui) -> programmation toujours en anglais


## Types de donnée

Entiers (integer/int) 
- - ∞ à + ∞ (rond)

Decimaux (float)
- - ∞ à + ∞
- (à virgule 3.14)

Chaîne de caractères (string/str)
- "entre guillemets"

Booléen (Boolean/Bool)
- True / False
- 1 / 0

## Les opérations

 Entiers:
- + addition
- - soustraction
- * multiplication
- // division entière
- / division -> résultat decimal
- ** -> puissance

String:
- + concatenation "Salut " + "ça va" = "Salut ça va"
- * multiplication en PYTHON uniquement "A" + 4 -> "AAAA"

Bool:
- AND --> ET
- OR --> OU                       = Opérateur Logiques
- NOT --> NON 

## Algèbre de Boole

| a   | b   | a ET b |
| --- | --- | ------ |
| F   | F   | F      |
| F   | V   | F      |
| V   | F   | F      |
| V   | V   | V      |
MULTIPLICATION

| a   | b   | a OU b |
| --- | --- | ------ |
| F   | F   | F      |
| F   | V   | V      |
| V   | F   | V      |
| V   | V   | V      |
ADDITION

| a   | NON a |
| --- | ----- |
| F   | V     |
| V   | F     |

EXERCICES :

|               | A   | B   | C   |
| ------------- | --- | --- | --- |
| a = 7         | 7   | X   | X   |
| b = 5         | 7   | 5   | X   |
| c = 2         | 7   | 5   | 2   |
| a = b * c     | 10  | 5   | 2   |
| c = a + a     | 10  | 5   | 20  |
| b = c * 3 - c | 10  | 40  | 20  |
| a = a + b + c | 70  | 40  | 20  |
| c = a - b + c | 70  | 40  | 50  |
a = 70, b = 40,  c = 50
