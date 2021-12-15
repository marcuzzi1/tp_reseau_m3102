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

