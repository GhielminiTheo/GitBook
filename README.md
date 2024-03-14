---
description: Documentation de mise en place d'hyper-v
---

# VIRT(1) - Hyper-V

### 1. Installation de l'AD et HYPER-V

Pour commencer,  j'ai installé le serveur Active Directory en interface graphique, puis j'ai installé le rôle Active Directory et fais la promotion du serveur en tant que contrôleur de domaine

<figure><img src=".gitbook/assets/promot.png" alt=""><figcaption><p>Création de la forêt et promotion en tant que contrôleur de domaine</p></figcaption></figure>

Une fois l'installation du serveur AD, j'ai procédé à la création des deux serveurs hyper-v. J'ai ensuite modifier leurs configuration IPs pour qu'ils puissent rejoindre le domaine créé précédemment.

Une fois les serveurs hyper-v ajouter dans l'AD, j'ai ajouté les outils RSAT pour le gestionnaire hyper-v afin de pourvoir les manager avec une interface graphique. J'ai également ajouter le gestionnaire de cluster de basculement afin de pouvoir créer et gérer mon cluster.

Avant de créer le cluster, j'ai installé le rôle "Serveur cible iSCSI" sur le serveur AD avec interface graphique, une fois le rôle installé. Avant de commence a créer les disques qui seront utiliser sur l'iSCSI, j'ai ajouter un disque de 160 GB qui servira pour le quorum et le stockage du cluster.&#x20;

Une fois le disque ajouter et les partitions deux partitions créées, j'ai configuré une cible iSCSI sur le serveur avec interface graphique. Pour se faire je suis allé dans le gestionnaire de serveur, puis "Services de fichiers et de stockage", puis iSCSI et j'ai créé deux disques, un de 150 GB (pour le stockage de des machines virtuelles) et un de 1 GB (pour le Quorum).  Une fois ceci fait,  j'ai créer la target iSCSI. J'ai ensuite configurer sur les serveur Hyper-V qui sont en mode core, l'initiateur iSCSI afin de connecter les serveurs au stockage du SAN grâce a la target créée précédemment.&#x20;

Pour ce faire, j'ai exécuté ces commandes sur le deux serveurs hyper-v

Pour commencer, démarrer le service MSiSCSI ainsi que de le passer en mode démarrage automatique.

```
Start-Service -Name MSiSCSI
Set-Service -Name MSiSCSI -StartupType Automatic 
```

Ensuite, j'ai dis sur quelle target je voulais me connecter sur le réseau "DATA" interne

```
New-IscsiTargetPortal -TargetPortalAddress "10.10.10.20"
```

Puis j'affiche la target avec cette commande afin de pouvoir la copier pour la prochaine commande

```
Get-IscsiTarget
```

Ensuite, je connecte le serveur avec la la target en entrant les données de la target (que j'ai créer lors de la création de la target)

```
Connect-IscsiTarget `
-NodeAddress iqn.1991-05.com.microsoft:vir1-ad-san-target01-target `
-AuthenticationType ONEWAYCHAP `
-ChapUsername "ChapUser" `
-ChapSecret "Pa$$w0rd" `
-IsPersistent $True
```

Une fois ceci fait, j'ai ensuite initialiser les deux partitions créées précédemment en commencent par le Quorum, en ligne de commande

```
Set-Disk -Number 1 -IsOffline $False
#initialisation du disque
Initialize-Disk -Number 1 -PartitionStyle GPT
#Vérification de la configuration
Get-Disk | Format-Table -AutoSize -Wrap
#Assignationd d'un lettre de lecteur a la partition 
New-Partition -DiskNumber 1 -UseMaximumSize -AssignDriveLetter
#Formatage de la partition au format NTFS
Format-Volume -DriveLetter E -FileSystem NTFS -Force
```

Une fois la target créée et fonctionnelle, j'ai été créer le cluster grâce au gestionnaire de cluster de basculement&#x20;
