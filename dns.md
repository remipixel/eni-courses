# Services DNS

Slide de présentation
Afficher titre, nom du sujet, nom de l'auteur
Comprendre la résolution de noms

## Définition

Un DNS est un service de résolution de noms. 
Il permet de convertir l'adressage IP des serveurs en chaine de caractères lisibles et faciles à retenir.

### Usages
Son usage se fait de manières : 
  - Le DNS privé : utilisé en interne sur un réseau privé (entreprise) pour des noms locaux
  - Le DNS public : permet de rendre accessibles au public des serveurs, notammenet des sites web, des services en ligne, etc. 

### Fonctionnement
Insérer un schéma fonctionnement de DNS


## Configuration d'un service DNS Linux
Bind9 est un service DNS historique et multiplateforme, Linux & Windows. 
Sa configuration se fati autour de 4 fichiers : 
- named.conf => utilisé pour les ACL
- named.conf.options => options actives pour toute la config
- named.conf.local => configurer les zones dns locales
- named.conf.default-zone => zones par défaut

### Installation du paquet
```bash
apt install bind9 -y
```
### Configuration des domaines

#### Définir les ACL (pour la sécurité, Access Control List)
```bash
nano named.conf
acl "monAclDeQualite" { 127.0.0.0/8; 192.168.1.0/24 }; //Permet de définir des sous réseaux autorisés à utiliser ce DNS
```
#### Choisir les options
```bash
allow-query { "monAclDeQualite"; };   //Définir quelles sont les ACL qui ont accès au DNS
allow-transfer { none; };             //Permet de d'autoriser ou non le transfert des zones sur les DNS maitres
dnssec-validation auto;               //Le DNSSEC est une version sécurisée du protocole
auth-nxdomain no;                     //Le message NXDOMAIN prévient si le domaine n'existe pas
directory "/etc/bind";                //Emplacement des fichiers de zone
listen-on-v6;                         //Permet de résoudre aussi pour les requetes ipv6
```
### Configuration des zones DNS
```bash
nano named.conf.local

// Déclaration de la zone « monsuperdomaine.top » :
zone "monsuperdomaine.top" {
type master;
file "/etc/bind/db.monsuperdomaine.top";
allow-update { none; };
};
```
### Configuration des enregistrements de zone
```bash
nano /etc/bind/db.monsuperdomaine.top //Emplacement du fichier des enregistrements de zone.

$TTL  86400
@ IN  SOA s1.monsuperdomaine.top.  admin.monsuperdomaine.top. (
                2022290801     ;Serial 10 chiffres logique
                604800         ;Refresh time
                86400          ;Retry
                2419200        ;Expiration de l'enregistrement si inexistant
                86400 )        ;Negative Cache TTL (erreurs)
                
@ IN  NS  s1.monsuperdomaine.top.
s1     IN A 192.168.1.10
srvdns IN A 192.168.1.100
srvweb IN A 192.168.1.101
dns1 IN  CNAME s1
```
## Configuration d'un service DNS avec Windows Server

