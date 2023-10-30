---
description: Configuration de Nextcloud
---

# Nextcloud

### Pour installer Nextcloud :

Mettre a jour le système

```
# apt-get update && apt-get upgrade
```

Installer apache2&#x20;

```
# apt-get install apache2 -y
```

Installer PHP&#x20;

{% code fullWidth="true" %}
```
# apt-get -y install php libapache2-mod-php php-mysql php-common php-gd php-xml php-mbstring php-zip php-curl
```
{% endcode %}

Installer MariaDB&#x20;

```
# apt-get -y install mariadb-server mariadb-client
```

Créer une base de donnée Nextcloud

```
# mysql -u root -p
et entrer un mot de passe
```

Dans MariaDB&#x20;

```
CREATE DATABASE nextcloud;
GRANT ALL PRIVILEGES ON nextcloud.* TO 'nextclouduser'@'localhost' IDENTIFIED BY 'Pa$$w0rd';
FLUSH PRIVILEGES;
EXIT;
```

Si ce n'est pas déjà fait installer le paquet wget

```
# apt-get install wget
```

Télécharger la dernière version de Nextcloud

```
# wget https://download.nextcloud.com/server/releases/nextcloud-27.1.2.zip
```

```
# unzip nextcloud-22.2.0.zip -d /var/www/html/
```

