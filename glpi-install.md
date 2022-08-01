# Installation de GLPI sur un serveur Debian 11

### Prérequis : 

- Serveur Debian 11 avec 4Go de RAM et au moins 1 core CPU et 20Go de disque

## Installer les paquets et dépendances

```
apt update && 
apt upgrade -y &&
apt install apache2 libapache2-mod-security2 mariadb-server php7.4 php7.4-mysql php7.4-mbstring php7.4-curl php7.4-gd php7.4-xml php7.4-ldap php7.4-xmlrpc php7.4-imap php7.4-intl php7.4-zip php7.4-bz2 php-apcu-bc php-cas
```

Rédemarrer le serveur apache : 
```systemctl restart apache2```

## Configuration de la base de données

Installation de mariadb-server 
```mysql_secure_installation```

- Ajouter un mot de passe root
- Change the root password : n
- Remove anonymous users : y
- Disallow root login remotely : y
- Remove test db : y 
- Reload privileges now : y

Se connecter au shell MySQL : 
```mysql -u root -p```

Créer un utilisateur : 
```CREATE USER 'new_user'@'localhost' IDENTIFIED BY 'password';```

Créer la base de données : 
```CREATE DATABASE glpidb;```

Vérifier l'existence de la base de données : 
```show databases;```

Donner les privilèges sur la base de données avec l'utilisateur créé : 
```grant all privileges on glpidb.* to new_user@localhost identified by 'password';```

Vérifier les privilèges sur la base de données : 
```show grants for new_user@localhost```

## Installation des fichiers 

Récupérer et télécharger les fichiers GLPI. 
https://github.com/glpi-project/glpi/releases

Extraire le fichier GLPI-xxxx.tar.gz dans le dossier /var/www avec 
```
tar -xvf /var/www/glpi-xxxx.tar.gz 
```

### Modifier l'emplacement des fichiers de GLPI

Créer un dossier glpi dans /etc
```
mkdir /etc/glpi
```

Créer le fichier local_define.php et complétez le avec ce code : 
```
<?php
define('GLPI_VAR_DIR', '/var/lib/glpi'); 
define('GLPI_DOC_DIR', GLPI_VAR_DIR); 
define('GLPI_CRON_DIR', GLPI_VAR_DIR . '/_cron');
define('GLPI_DUMP_DIR', GLPI_VAR_DIR . '/_dumps');
define('GLPI_GRAPH_DIR', GLPI_VAR_DIR . '/_graphs');
define('GLPI_LOCK_DIR', GLPI_VAR_DIR . '/_lock'); 
define('GLPI_PICTURE_DIR', GLPI_VAR_DIR . '/_pictures');
define('GLPI_PLUGIN_DOC_DIR', GLPI_VAR_DIR . '/_plugins');
define('GLPI_RSS_DIR', GLPI_VAR_DIR . '/_rss'); 
define('GLPI_SESSION_DIR',     GLPI_VAR_DIR . '/_sessions');
define('GLPI_TMP_DIR', GLPI_VAR_DIR . '/_tmp'); 
define('GLPI_UPLOAD_DIR', GLPI_VAR_DIR . '/_uploads');
define('GLPI_CACHE_DIR', GLPI_VAR_DIR . '/_cache');
define('GLPI_LOG_DIR', '/var/log/glpi');
?>
```

Donner les droits en récursif sur /etc/glpi et /var/www/glpi/files avec l'utilisateur www-data ou un utilisateur du groupe www-data
```
chown -R www-data: /etc/glpi
chown -R www-data: /var/www/glpi/files
```

Créer un répertoire /var/lib/glpi
```
mkdir /var/lib/glpi
```

Copier les fichiers de /var/www/glpi/files dedans 
```
cp /var/www/glpi/files /var/lib/glpi
```

Donner les droits en récursif sur le dossier
```
chown -R www-data: /var/lib/glpi
```

Vérifier les droits avec ```ls -l /var/lib/glpi```

Créer un répertoire /var/log/glpi
```
mkdir /var/log/glpi
```

Donner les droits en récursif sur le dossier
```
chown -R www-data: /var/log/glpi
```

Créer un fichier /var/www/glpi/inc/downstream.php
```
<?php
define('GLPI_CONFIG_DIR', '/etc/glpi/');
if (file_exists(GLPI_CONFIG_DIR . '/local_define.php')) {
      require_once GLPI_CONFIG_DIR . '/local_define.php'; 
}
?>
```

Donner les droits en récursif sur le dossier /var/www/glpi/marketplace et vérifier
``` 
chown -R www-data: /var/www/glpi/marketplace
```
