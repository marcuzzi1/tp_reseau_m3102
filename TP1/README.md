# TP 1
---
Voici donc notre premier TP ! Lançons nous maintenant dans le dur :smile:
## Création du fichier lab.conf

Pour ce fichier, rien de particulier à signaler, je vais simplement créer mes réseaux et y lier mes machines :

```conf
# Routeurs
r0[0]=net0
r0[1]=net1

r1[0]=net1
r1[1]=net2

# Machines de net0
pca[0]=net0
pcb[0]=net0

# Machines de net1
pcc[0]=net1

# Machines de net2
pcd[0]=net2
```

### Premier lancement du LAB
Placez-vous dans le répertoire contenant votre TP1 et ses fichiers depuis un terminal puis exécutez la commande suivante : 
```bash
$ kathara lstart
```
Maintenant vous devriez voir autant de terminaux que de machines sur le schéma apparaître.

#### Le dossier `shared`
Si par défaut le lancement du LAB vous créé un dossier `shared`, pas de panique c'est normal. Dans le cas contraire, si toutefois vous en avez besoin vous pouvez toujours le créer et Kathara le montera automatiquement aux machines lors du démarrage du LAB.

#### La connectivité
Maintenant, vous souhaitez peut-être faire un `ping` entre machines, mais vous ne pourrez pas... On n'a pas encore ajouté les adresses IP !

---
## Les fichiers de démarrage, ou fichier `.startup`
Les fichiers de démarrage sont nommés de la manière suivante : `machine.startup` et sont des fichiers contenant des instructions bash qui vont s'exécuter au lancement du lab sur chaque machine concernée.

C'est celui-ci que l'on va utiliser pour ajouter par exemple les adresses IP, les routes...

### Les IP et les routes
Pour ajouter les IP, on définie une adresse et son masque sur une interface, puis on active cette interface
#### pca.startup
Selon la topologie, la route par défaut de cette machine a besoin d'être R0
```conf
ip a add 192.168.1.1/24 dev eth0
ip link set eth0 up
ip route add default via 192.168.1.254
```

#### pcb.startup
Ici, même chose que pour PCA, c'est R0 que nous mettrons en routeur par défaut
```conf
ip a add 192.168.1.2/24 dev eth0
ip link set eth0 up
ip route add default via 192.168.1.254
```

#### pcc.startup
Pour cette machine, c'est un peu plus spécial puisqu'elle est contenue dans un réseau où se trouvent R0 et R1. Il va donc falloir mettre en place une route pour les réseaux de chacun. J'ai donc fait le choix de définir R1 en routeur par défaut et d'ajouter une route vers le réseau 192.168.1.0/24 par R0.
```conf
ip a add 172.16.5.1/24 dev eth0
ip link set eth0 up
ip route add default via 172.16.5.254
ip route add 192.168.1.0/24 via 172.16.5.253
```
Avec cette configuration vous devriez être capable d'accéder à PCA et PCB depuis PCC me direz-vous... Eh bien non ! Tant que l'on n'a pas configuré les routeurs cette manipulation est impossible.

