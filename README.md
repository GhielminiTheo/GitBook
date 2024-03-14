---
description: Documentation de mise en place d'hyper-v
---

# VIRT(1) - Hyper-V

### 1. Installation de l'AD et HYPER-V

Pour commencer,  j'ai installé le serveur Active Directory en interface graphique, puis j'ai installé le rôle Active Directory et fais la promotion du serveur en tant que contrôleur de domaine

<figure><img src=".gitbook/assets/promot.png" alt=""><figcaption><p>Création de la forêt et promotion en tant que contrôleur de domaine</p></figcaption></figure>

Une fois l'installation du serveur AD, j'ai procédé à la création des deux serveurs hyper-v. J'ai ensuite modifier leurs configuration IPs pour qu'ils puissent rejoindre le domaine créé précédemment.

Une fois les serveurs hyper-v ajouter dans l'AD, j'ai ajouté les outils RSAT pour le gestionnaire hyper-v afin de pourvoir les manager avec une interface graphique. J'ai également ajouter le gestionnaire de cluster de basculement afin de pouvoir créer et gérer mon cluster.

Avant de créer le cluster, j'ai installé le rôle "iSCSI Target Server" sur le serveur AD avec interface graphique, une fois le rôle installé. Avant de commence a créer les disques qui seront utiliser sur l'iSCSI&#x20;

