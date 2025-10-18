Permet de contenir plusieurs valeurs

chats = ["bibou", "tartuffe", "frimouse"]
divers = ["a", 12, True, 3.14]

l = [1, 2, 3, 4]  pour acceder  on utilise son indice
print (l[2]) # affiche 3
print (len(l)) # affiche 4

last index = len(l) - 1 (savoir dernier indice)

## PARCOURS D'UNE LISTE

fruits = ["pomme", "fraise", "banane"]
for i in range (0, len(fruits)):
		print(fruits[i])

vegetables = ["aubergine", "brocolis", "haricot"]
for vegetable in vegetables:
			print(vegetable)