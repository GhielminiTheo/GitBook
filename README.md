---
description: Configuration des VMs serveur 01 et 02
---

# Configuration de srv-lin1-01 et srv-lin1-02

## Configuration réseau SRV-LIN1-01

IMPORTANT : installation et utilisation du sudo avant chaque commandes pour avoir les droits administrateur sur un autre utilisateur que l'utilisateur root

Configuration des interfaces réseaux&#x20;

```
#nano /etc/network/interfaces
        # The primary interface INTERNET
        auto ens34
        iface ens34 inet DHCP
        
        # The secondary interface LOCAL
        auto ens33
        iface ens33 inet static
        address 10.10.10.11/24
```

Configuration du nom de la machine

```
#hostnamectl set-hostname srv-lin1-01.lin1.local
#hostname -f
```

Configuration du fichier resolv.conf&#x20;

```
#nano /etc/resolv.conf
    domain lin1.local
    search lin1.local
    nameserver 10.10.10.11
    nameserver 1.1.1.1
```

Restart de la machine pour appliquer les modifications

```
#systemctl restart networking.service
#apt -y update && apt upgrade
```

## Configuration NAT

Activation de l'option ipforwarding pour que le serveur puisse router sur les autres machines du domaine.

<pre><code><strong>#echo 'net.ipv4.ip_forward=1' >> /etc/sysctl.conf
</strong>#sysctl -p /etc/sysctl.conf
</code></pre>

Installation d'iptables

<pre><code><strong>#apt install iptables
</strong>#iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE

#apt install -y iptables-persistent
/sbin/iptables-save > /etc/iptables/rules.v4
</code></pre>

## Configuration DNS : dnsmasq

Installation de l'outil dnsmasq

```
# apt-get -y install dnsmasq
```

Configuration du fichier dnsmasq.conf

```
#nano /etc/dnsmasq.conf
    address=/srv-lin1-01.lin1.local/srv-lin1-01/10.10.10.11
    address=/srv-lin1-02.lin1.local/srv-lin1-02/10.10.10.22
    address=/nas-lin1-01.lin1.local/nas-lin1-01/10.10.10.33
    
    ptr-record=11.10.10.10.in-addr.arpa.,"srv-lin1-01"
    ptr-record=22.10.10.10.in-addr.arpa.,"srv-lin1-02"
    ptr-record=33.10.10.10.in-addr.arpa.,"nas-lin1-01"
```

Restart du service afin d'appliquer les modifications

```
#systemctl restart dnsmasq.service
```

## Configuration de srv-lin1-02

Configuration de  l'interface réseau&#x20;

```
#nano /etc/network/interfaces
  # Interface ens33 LOCAL
  auto ens33
  iface ens33 inet static
  address 10.10.10.22/24
  gateway 10.10.10.11
```

Configuration du nom de la machine

<pre><code><strong>#hostnamectl set-hostname srv-lin1-02.lin1.local
</strong><strong>#hostname -f
</strong></code></pre>

Configuration du fichier resolv.conf&#x20;

<pre><code><strong>#nano /etc/resolv.conf
</strong><strong>    domain lin1.local
</strong><strong>    search lin1.local
</strong><strong>    nameserver 10.10.10.11
</strong></code></pre>
