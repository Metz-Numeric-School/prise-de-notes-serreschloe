
![[Pasted image 20250115135441.png]]

SW-01 [SWITCH ] : 
Show vlan br 
conf t 
int range e1/0-3 
sw mo ac 
sw ac vlan 10 
exit
int range e2/0-3 
sw mo ac 
sw ac vlan 50 
exit 
show int tr 
"control z" 
wr


SW-02 [SWITCH ] : 
Show vlan br 
conf t 
int range e1/0-3 
sw mo ac 
sw ac vlan 20 
exit
int range e2/0-3 
sw mo ac 
sw ac vlan 50 
exit 
show int tr 
"control z" 
wr

SW-03 [SWITCH ] : 
Show vlan br 
conf t 
int range e1/0-3 
sw mo ac 
sw ac vlan 30 
exit
int range e2/0-3 
sw mo ac 
sw ac vlan 40 
exit 
int range e3/0-3 
sw mo ac 
sw ac vlan 50 
exit
int range e4/0-3 
sw mo ac 
sw ac vlan 60 
exit
show int tr 
"control z" 
wr

Calcul pour les ACLs (Access-list)

255 . 255 . 255 . 255     /26
255 . 255 . 255 . 192
0   .   0   .  0   .  63 


255 . 255 . 255 . 255     /28
255 . 255 . 255 . 240
0   .   0   .  0   .  15 

