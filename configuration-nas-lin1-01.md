---
description: OpenMediaVault
---

# Configuration nas-lin1-01

Configuration réseau de nas-lin1-01

```
nano /etc/network/interfaces
  # Interface ens33 LOCAL
  auto ens33
  iface ens33 inet static
  address 10.10.10.33/24
  gateway 10.10.10.11
```

Configuration du nom de la machine

```
#hostnamectl set-hostname nas-lin1-01.lin1.local
#hostname -f
```

Appliquer les modifications

```
# Reboot
```
