# Installation de GLPI sur un serveur Debian 11

### Prérequis : 

- Serveur Debian 11 avec 4Go de RAM et au moins 1 core CPU et 20Go de disque

## Installer les paquets et dépendances

```
apt update && 
apt upgrade -y &&
apt install apache2 libapache2-mod-security2 mariadb-server php7.4 php7.4-mysql php7.4-mbstring php7.4-curl php7.4-gd php7.4-xml php7.4-ldap php7.4-xmlrpc php7.4-imap php7.4-intl php7.4-zip php7.4-bz2 php-apcu-bc php-cas
```

Rédemarrer le serveur apache `systemctl restart apache2`

## Configuration de la base de données

Installation de mariadb-server `mysql_secure_installation`

- Ajouter un mot de passe root
- Change the root password : n
- Remove anonymous users : y
- Disallow root login remotely : y
- Remove test db : y 
- Reload privileges now : y

Se connecter au shell MySQL : `mysql -u root -p`
Créer un utilisateur : `CREATE USER 'new_user'@'localhost' IDENTIFIED BY 'password';`
Créer la base de données : `CREATE DATABASE glpidb;`
Vérifier l'existence de la base de données : `show databases;`
Donner les privilèges sur la base de données avec l'utilisateur créé : `grant all privileges on glpidb.* to new_user@localhost identified by 'password';`
Vérifier les privilèges sur la base de données : `show grants for new_user@localhost`

