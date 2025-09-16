# Virtual Local Area Network
Les VLANs sont des sous-réseaux **logiques** sur la **couche 2** (data link / liaison de données) répartis sur le [LAN](WAN-MAN-LAN-PAN#LAN).

Contrairement à un LAN traditionnel où tous les appreils sont sur la même plage de diffusion (broadcasting) *todo verif ce vocab*, un VLAN permet de regrouper des appareils en focntion de critères comme la fonction, le département ou la sécurité. Chaque VLAN est indépendant.
![[Pasted image 20250820142634.png]]
### Trunks
Faire passer plusieurs vlan sur une même connexion physique. interconnexion de vlan, avec maintien de l'imperméabilité. Ca marche grâce au **tag VLAN** 
=> Les trunks sont tagged, les vlan sont untagged
## Avantages
### Optimisation des performances
par réduction de la taille des domaines de diffusion, pas de diffusion inutile => meilleur temps de réponse, moins de latence
### Sécurité renforcée
limitation d'accès aux ressources aux bonnes parties prenantes, car 1 vlan = 1 entité indépendante
### Coûts réduits
car on fait passer dans un meme réseau physique plusieurs réseaux logiques, ce qui décuple les flux d'info avec les memes équipements réseauw => moins de dépenses
### Gestion flexible
on recable pas le réseau, il suffit de changer la config du vlan

## Sources
vidéo cookie connecté https://www.youtube.com/watch?v=Eh9INNkMM4I&list=PLP0aqyZ5GFdlb7MtCHYNZwUlGhY1BkMS_&index=4