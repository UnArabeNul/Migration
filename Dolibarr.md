Avant de commencer
```
apt-get update && apt-get upgrade
```


# Apache

## Installer un serveur Apache
```
apt-get install -y apache2
```

## Pour que Apache démarre en meme temps que le systeme
```
systemctl enable apache2
```

## Pour tester le serveur
```
ip a
```
Puis sur rechercher l'ip sur un navigateur sur le meme reseau

## Pour voir la version d'Apache
```
apache2ctl -v
```

## Module Apache utile
```
a2enmod rewrite #module utilisé pour la réécriture d'URL
a2enmod deflate #module pour la gestion de la compression, notamment en gzip, pour utiliser la mise en cache des pages sur votre site
a2enmod headers #module pour agir sur les en-têtes HTTP
a2enmod ssl #module pour gérer les certificats SSL et donc l'utilisation de HTTPS
```

## Après avoir activé ou désactivé un module il faut redémarrer le service Apache
```
systemctl restart apache2
```

## Fichier de configuraton d'Apache
```
/etc/apache2/apache2.conf
```

## Fichier où déclarer les Virtual Hosts
```
/etc/apache2/sites-available
/etc/apache2/sites-enabled
```

# PHP

## Installation des dépendances

```
apt-get install ca-certificates apt-transport-https software-properties-common wget curl lsb-release
```

## Ajouter le dépôt pour PHP 8.1

```
curl -sSL https://packages.sury.org/php/README.txt | bash -x
```

## Installation de PHP 8.1

```
apt-get install php8.1
```

## Intégration de PHP à Apache

```
apt-get install libapache2-mod-php8.1
```
puis il faut redemarrer Apache

```
systemctl restart apache2
```

## Vérification de la version PHP

```
php -v
```

## Installation des extensions de PHP 8.1

```
apt-get install php8.1-common php8.1-curl php8.1-bcmath php8.1-intl php8.1-mbstring php8.1-xmlrpc php8.1-mcrypt php8.1-mysql php8.1-gd php8.1-xml php8.1-cli php8.1-zip php8.1-fpm libapache2-mod-fcgid
```

## Activation de PHP-FPM, pour améliorer les performances, en ajustant la configuration d'Apache

```
a2enmod proxy_fcgi setenvif
a2enconf php8.1-fpm
```

puis il faut redemarrer Apache

```
systemctl restart apache2
```

# Dolibarr

