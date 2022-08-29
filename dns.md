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
- 

### Installation du paquet
```
apt install bind9 -y
```
### Configuration des domaines


```

```
### Configuration des zones DNS
```

```

### 
## Configuration d'un service DNS avec Windows Server
