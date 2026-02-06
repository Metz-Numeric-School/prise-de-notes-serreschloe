# PowerShell

![[Pasted image 20251121084855.png]]

Objet = Ensemble d'attributs

Pour filtrer les 5 premiers éléments de ma liste

![[Pasted image 20251121085859.png]]

Pour avoir les ID supérieur à 0 

![[Pasted image 20251121090513.png]]

Commande pour voir toutes les commandes 

![[Pasted image 20251121090910.png]]

Toutes les commandes ou il y a "file" dans la commande

![[Pasted image 20251121091036.png]]

Pour avoir toutes les informations sur une commande

![[Pasted image 20251121091403.png]]

Commande h est un alias

![[Pasted image 20251121091433.png]]

Pour lister tous les alias

![[Pasted image 20251121091520.png]]

Exercice : Lister les 5 premiers process qui commencent par "W"

Get-Process | Where-Object { $_.Name -like "W*" } | Select-Object -First 5
Get-Process W* | Select-Object -First 5

![[Pasted image 20251121092107.png]]

$name = "John Doe" -> création de variable Name 
Write-Host pour écrire 

![[Pasted image 20251121093709.png]]

Out-File -> sauvegarder dans un fichier

Exercice : Lister les 20 Process qui consomment le plus de CPU. Afficher : Id, Name, CPU, Path. Puis exporter en CSV

Get-Process | Sort-Object CPU -Descending | Select-Object Id,Name,CPU,Path -First 20 | Export-Csv "process_top20_cpu.csv" -NoTypeInformation


![[Pasted image 20251121105000.png]]


Exercice : Dans le dossier de votre User, lister les 10 plus gros fichier

Aide : Set-Location, Get-ChildItem

Set-Location $HOME; 
Get-ChildItem -File -Recurse | Sort-Object Length -Descending | Select-Object -First 10 Name, FullName, Length

![[Pasted image 20251121114915.png]]

