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
