---
description: Documentation de mise en place d'hyper-v
---

# VIRT(1) - Hyper-V

### 1. Installation de l'AD et HYPER-V

Pour commencer,  j'ai installé le serveur Active Directory en interface graphique, puis j'ai installé le rôle Active Directory et fais la promotion du serveur en tant que contrôleur de domaine

<figure><img src=".gitbook/assets/promot.png" alt=""><figcaption><p>Création de la forêt et promotion en tant que contrôleur de domaine</p></figcaption></figure>

Une fois l'installation du serveur AD, j'ai procédé à la création des deux serveurs hyper-v. J'ai ensuite modifier leurs configuration IPs pour qu'ils puissent rejoindre le domaine créé précédemment.

Une fois les serveurs hyper-v ajouter dans l'AD,&#x20;
