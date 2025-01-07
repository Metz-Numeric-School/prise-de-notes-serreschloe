
## Création de VLANs

int range F0/1-8
switchport mode access
switchport access vlan 10

int range F0/9-16
switchport mode access
switchport access vlan 20

int range F0/17-24
switchport mode access
switchport access vlan 30

VLAN 10 -> administration
VLAN 20 -> Employes
VLAN 3O -> Invites

## Mode TRUNK

