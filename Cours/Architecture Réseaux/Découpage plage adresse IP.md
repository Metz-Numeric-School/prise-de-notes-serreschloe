![[Pasted image 20250106140901.png]]


**/12 -> compter 12 de gauche à droite**
### Pour savoir la première adresse, il faut tout mettre à 0 

adresse 10101000.11000000.00100101.00100001
masque 11111111.11110000.00000000.00000000
calcul 10101000.11000000.00000000.00000000 -> 168.192.0.0

### Pour savoir la dernière adresse, il faut mettre tous les 0 à 1 

adresse 10101000.11000000.00100101.00100001
masque 11111111.11110000.00000000.00000000
calcul 10101000.11001111.11111111.11111111 -> 168. 207. 255 . 255

Capacité maximal Classe A = Subnet mask classe A = /8
Capacité maximal Classe B  = Subnet mask classe B = /12
Capacité maximal Classe C = Subnet mask classe C = /16


