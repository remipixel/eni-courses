# Création de sites sur Apache

## Etape 1 : enregistrement DNS


## Etape 2 : création du fichier de configuration dans /etc/apache2/site-available 

```
<VirtualHost *:80>

    ServerName wwa.gcheramy.gch
    DocumentRoot /var/www/wwa.gcheramy.gch

    <Directory /var/www/wwa.gcheramy.gch >
      Require all granted
    </Directory>

</VirtualHost>
```

## Etape 3 : création de l'hébergement des données 

```
cd /var/www
mkdir wwa.gcheramy.gch
```

### Création du fichier index.html 

nano wwa.gheramy.gch/index.html

```
<html>
        <head>
                <title>Mon site internet wwa</title>
        </head>

        <body>
                <h1>Site wwa</h1>
                <p>Ce site est le meilleur site du monde</p>
        </body>


</html>
```

### Création de l'utilisateur :
```
useradd -s /bin/false -d /var/www/wwa.gcheramy.gch/ wwa
```

### Changement des droits
```
chown -R wwa: wwa.gcheramy.name 
find ./wwa.gcheramy.name -type d -exec chmod 2770 {} \;
find ./wwa.gcheramy.name -type f -exec chmod 660 {} \;
usermod -aG wwa www-data
```

### Activation du site
```
a2ensite wwa.gcheramy.name
```

### Vérification 
```
apachectl -S
```

### Vérification à partir d'un navigateur

# Faire tourner un site sur une IP et un port particulier sous Apache

## Créer IP supplémentaire sur le server 
-> Fichier /etc/network/interfaces
-> Restart réseau

## Fichiers ports.conf Apache

Ajouter la ligne : 
```
Listen 192.168.1.2:81
```

##Ficheirs de conf du site
/etc/apache2/sites-available/192.168.1.2.conf
```
<VirtualHost 192.168.1.2:81>
    DocumentRoot /var/www/192.168.55.2
    <Directory /var/www/192.168.55.2>
        Require all granted
    </Directory>
</VirtualHost>
```
