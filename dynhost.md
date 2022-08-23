# Connecter un nom de domaine sur sa box

Nous allons intégrer un nom de domaine directement sur la Livebox grâce au service DynHost inclus qui permet de faire du DynDNS. 

## Configurer le nom de domaine depuis l'hébergeur OVHcloud

Connectez-vous à votre espace client OVHcloud puis accédez à l'interface de gestion du nom de domaine.
Allez dans l'onglet DynHost (service DynDNS intégré à OVH). 

### Ajouter un nouvel accès dans DynHost

Cliquez sur le bouton "Gérer les accès" pour configurer un nouvel accès. 
Vous allez configurer trois éléments :
- Le nom d'utilisateur au format "monsuperdomaine.fr-nomdutilisateur"
- Le sous-domaine associé (vous pouvez laisser ce champ vide, mais choisissez-en un par souci d'organisation) exemple : mordor.monsuperdomaine.fr
- Le mot de passe associé (pour la sécurité de la connexion)

### Configurer le service DynHost avec votre IP publique actuelle

Récupérez votre IP publique via l'interface de votre box ou votre routeur. 
Sinon allez directement sur ce site : http://monip.org/

Cliquez sur le bouton "Ajouter un DynHost" et renseignez :
- Le sous-domaine tout juste créé
- L'adresse IP publique de votre box ou routeur

Sauvegardez. 

## Configurer le DynDNS sur le routeur

### Se connecter à l'interface de votre box ou routeur

#### Livebox
Se connecter à l'interface de la Livebox avec l'IP http://192.168.1.1/
> L'identifiant par défaut est "admin"
> Le mot de passe par défaut est sur le sticker sous la box (changez-le)

Configurer le service : 
- Allez dans la catégorie "Réseau"
- Ouvrez l'onglet DynDNS
- Choisissez un service DynDNS
- Choisissez comme hôte le sous domaine précédemment créé (mordor.monsuperdomaine.fr)
- Nom d'utilisateur complet (monsuperdomaine.fr-nomdutilisateur)
- Le mot de passe choisi pour l'accès

Enregistrez.

## Tester la configuration

Pour tester le bon fonctionnement et renouveler votre IP publique, il suffit de redémarrer votre box.
Dans la console de gestion OVH, vérifiez que l'IP publique a bien été modifiée aussi.

**Attention : La propagation DNS pouvant être longue, vous devrez peut-être attendre quelques minutes pour accéder à vos serveurs via votre nom de domaine.**

Pour en savoir + sur DynHost avec OVH : https://docs.ovh.com/fr/domains/utilisation-dynhost/
Configurer le DynDNS sur la Livebox 4/5 : https://assistance.orange.fr/livebox-modem/toutes-les-livebox-et-modems/installer-et-utiliser/piloter-et-parametrer-votre-materiel/le-parametrage-avance-reseau-nat-pat-ip/dns/livebox-configurer-un-service-dns-dynamique_188820-730441
Configurer l'accès à serveur hébergé derrière une Livebox : https://assistance.orange.fr/livebox-modem/toutes-les-livebox-et-modems/installer-et-utiliser/piloter-et-parametrer-votre-materiel/le-parametrage-avance-reseau-nat-pat-ip/dns/livebox-le-loopback_243342-785338
