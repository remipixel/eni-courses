# Création de sites sur Apache

## Bonnes pratiques 

Créer un utilisateur et gorupe pour chaque site hébergé 
useradd -s /bin/false -d /var/www/dossierdusite wwa 

(on crée user pour chaque site avec le dossier du site comme repertoire par défaut et shell desactivé et nom=nomdusite)
et faire chown -R usernomdusite: /var/www/repertoiredusite (crée user et groupe) + 
Ajouter www-data dans chaque groupe de site créé. 

Faire des chmod 660 sur les fichiers et 2770 sur les dossiers a l'aide de find
find ./ -type d -exec chmod 2770 {} \; (dossiers)
find ./ -type f -exec chmod 660 {} \; (fichiers)

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
