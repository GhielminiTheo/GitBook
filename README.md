---
description: Configuration des VMs
---

# Lin1

## Configuration réseau SRV-LIN1-01

sudo pour avoir les droits administrateur sur un autre utilisateur que l'utilisateur roo

```
#nano /etc/network/intterfaces
        # The primary interface INTERNET
        auto ens34
        iface ens34 inet DHCP
        
        # The secondary interface LOCAL
        auto ens33
        iface ens33 inet static
        address 10.10.10.11/24
```



```
#hostnamectl set-hostname srv-lin1-01.lin1.local
#hostname -f
```

```
#nano /etc/resolv.conf
    search lin1.local
    nameserver 10.10.10.11
    nameserver 1.1.1.1
```

```
#systemctl restart networking.service
#apt -y update && apt upgrade
```

## Configuration NAT

<pre><code><strong>#echo 'net.ipv4.ip_forward=1' >> /etc/sysctl.conf
</strong>#sysctl -p /etc/sysctl.conf
</code></pre>

<pre><code><strong>#apt install iptables
</strong>#iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE

#apt install -y iptables-persistent
/sbin/iptables-save > /etc/iptables/rules.v4
</code></pre>

## Configuration DNS : dnsmasq

```
#apt -y install dnsmasq
```

```
#nano /etc/dnsmasq.conf
    address=/SRV-LIN1-01.lin1.local/SRV-LIN1-01/10.10.10.11
    address=/SRV-LIN1-02.lin1.local/SRV-LIN1-02/10.10.10.22
    address=/NAS-LIN1-01.lin1.local/NAS-LIN1-01/10.10.10.33
    
    ptr-record=11.10.10.10.in-addr.arpa.,"SRV-LIN1-01"
    ptr-record=22.10.10.10.in-addr.arpa.,"SRV-LIN1-02"
    ptr-record=33.10.10.10.in-addr.arpa.,"NAS-LIN1-01"
```

```
#systemctl restart dnsmasq.service
```

## Configuration des autres serveurs

```
#nano /etc/network/interfaces
  # Interface xxxx LOCAL
  auto xxxx
  iface xxxx inet static
  address 10.10.10.xx/24
  gateway 10.10.10.11
```

<pre><code><strong>#hostnamectl set-hostname xxx-lin1-xx.lin1.local
</strong></code></pre>

<pre><code><strong>#nano /etc/resolv.conf
</strong><strong>    search lin1.local
</strong><strong>    nameserver 10.10.10.11
</strong></code></pre>
