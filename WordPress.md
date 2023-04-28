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


# MariaDB

## Installer MariaDB

```
apt-get install -y mariadb-server
```

## Exécuter le script "mariadb-secure-installation" afin de sécuriser un minimum votre installation de MariaDB

```
mariadb-secure-installation
```

Mettre "y" a tout et mémoriser le nouveau mot de passe

## Vérification de la version de MariaDB

```
mariadb -V
```

ou

```
apt policy mariadb-server
```

## Après un changement de configuration de MariaDB

```
systemctl restart mariadb
```

# WordPress

## Télécharger la derniere version de WordPress

Ce positionner dans le fichier "/tmp"

```
cd /tmp
```

Télécharger la derniere version de WordPress

```
wget https://wordpress.org/latest.zip
```

## Créer une base de données pour WordPress

Ce connecter à MariaDB

```
mariadb -u root -p
```
Renseigner le mot de passe de l'utilisateur root de la base de données

### Première étape : la création de la base de données

```
CREATE DATABASE WordPress;
```

### Deuxième étape : créer l'utilisateur qui sera administrateur de la base de données WordPress

```
CREATE USER 'admin'@'localhost' IDENTIFIED BY 'admin';
```

### Troisième étape : donner tous les droits à l'utilisateur "admin" sur la base de données WordPress.

```
GRANT ALL PRIVILEGES ON WordPress.* TO admin@localhost;
```

Enfin, il faut exécuter la commande suivante pour actualiser les droits et activer les nouveaux privilèges sur notre base de données

```
FLUSH PRIVILEGES;
```

Puis quitter MariaBD

```
exit
```

## Décompresser l'archive WordPress à la racine du site

Au préalable, on supprime la page d'index créée par défaut par Apache

```
rm /var/www/html/index.html
```

Ensuite, on installe le paquet « zip » sur notre serveur pour pouvoir décompresser l’archive de WordPress

```
apt-get install zip
```

On décompresse l'archive dans "/var/www/html"

```
unzip latest.zip -d /var/www/html
```
L'option "-d" permet de définir là où sera décompressée l'archive.
Le dossier WordPress apparaitra donc dans "/var/www/html" qui est le dossier où sont stockées les pages web par défaut.

Ce déplacer dans le dossier "/var/www/html" 

```
cd /var/www/html
```

Ensuite, exécutez la commande ci-dessous pour déplacer tout le contenu du dossier "wordpress" à la racine de notre site

```
mv wordpress/* /var/www/html/
```

Puisque le dossier "wordpress" ne sert plus à rien, on va le supprimer

```
rm wordpress/ -Rf
```

Enfin, on termine en donnant les droits à l'utilisateur "www-data" (correspondant à Apache) sur tous les fichiers de notre site, de manière récursive

```
chown -R www-data:www-data /var/www/html/
```

## Continuer l'installation de maniere graphique sur un navigateur

En cas d'erreur MySQL

```
apt-get install mysql
```

## Installer l'extention "Stockage Microsoft Azure pour WordPress"
