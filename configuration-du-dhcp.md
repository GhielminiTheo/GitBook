---
description: Configuration du fichier dnsmasq.conf
---

# Configuration du DHCP

Configuration du fichier dnsmasq.conf afin que l'outil dnsmasq puisse servir de DHCP pour fournir une adresse automatiquement aux machines clientes.

```
#domain-needed
#bogus-priv
#filterwin2k

#localise-queries
#local=/lan/
domain=lin1.local
#expand-hosts
#no-negcache
#resolv-file=/tmp/resolv.conf.auto

dhcp-authoritative
dhcp-leasefile=/tmp/dhcp.leases
#use /etc/ethers for static hosts; same format as --dhcp-host
read-ethers
#Plage DHCP
dhcp-range=10.10.10.110,10.10.10.119,12h
#Netmask
dhcp-option=1,255.255.255.0
#Route
dhcp-option=6,10.10.10.11
dhcp-option=3,10.10.10.11
#Bind Interface ens33
interface=ens33
```

Commandes restart

```
#/etc/init.d/dnsmasq restart
```
