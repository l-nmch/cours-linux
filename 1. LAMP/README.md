# Installation de LAMP

Dans ce cours nous allons voir comment installer [LAMP](https://fr.wikipedia.org/wiki/LAMP) sur une machine Debian 12

## Pré-requis

- Une machine virtuelle Debian 12 disposant d'un accès internet

## TP

Voici la suite de commande attendu pour installer LAMP sur votre VM

1. Mise à jour des sources

  ```sh
  sudo apt update
  sudo apt upgrade -y
  sudo apt install nano wget curl -y # Installation des commandes de base
  ```

2. Installation de Apache2

  ```sh
  sudo apt install -y apache2
  sudo systemctl enable apache2 # Activation du service
  ```

3. Ajout des modifications Apache2 nécéssaires au bon fonctionnement de LAMP

  ```sh
  sudo a2enmod rewrite
  sudo a2enmod deflate
  sudo a2enmod headers
  sudo a2enmod ssl
  sudo systemctl restart apache2 # Redémarrage du service
  ```

4. Installation des dépendences PHP

  ```sh
  sudo apt install -y apache2-utils php php-pdo php-mysql php-zip php-gd php-mbstring php-curl php-xml php-pear php-bcmath
  ```

5. Création d'un fichier PHP de test

  ```sh
  sudo nano /etc/www/html/phpinfo.php
  ```

  ```
  <?php
  phpinfo();
  ?>
  ```

6. Installation de MariaDB

  ```sh
  sudo apt install -y mariadb-server
  ```

7. Configuration de MariaDB

  ```sh
  sudo mariadb-secure-installation
  ```
    
  ```
  NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
  SERVERS IN PRODUCTION USE! PLEASE READ EACH STEP CAREFULLY!
  
  In order to log into MariaDB to secure it, we'll need the current
  password for the root user. If you've just installed MariaDB, and
  haven't set the root password yet, you should just press enter here.
  
  Enter current password for root (enter for none):
  OK, successfully used password, moving on...
  
  Setting the root password or using the unix_socket ensures that nobody
  can log into the MariaDB root user without the proper authorisation.
  
  You already have your root account protected, so you can safely answer 'n'.
  
  Switch to unix_socket authentication [Y/n] n
  ... skipping.
  
  You already have your root account protected, so you can safely answer 'n'.
  
  Change the root password? [Y/n] Y
  New password: **************
  Re-enter new password: **************
  Password updated successfully!
  Reloading privilege tables..
  ... Success!
  
  
  By default, a MariaDB installation has an anonymous user, allowing anyone
  to log into MariaDB without having to have a user account created for
  them. This is intended only for testing, and to make the installation
  go a bit smoother. You should remove them before moving into a
  production environment.
  
  Remove anonymous users? [Y/n] y
  ... Success!
  
  Normally, root should only be allowed to connect from 'localhost'. This
  ensures that someone cannot guess at the root password from the network.
  
  Disallow root login remotely? [Y/n] y
  ... Success!
  
  By default, MariaDB comes with a database named 'test' that anyone can
  access. This is also intended only for testing, and should be removed
  before moving into a production environment.
  
  Remove test database and access to it? [Y/n] y
  - Dropping test database...
  ... Success!
  - Removing privileges on test database...
  ... Success!
  
  Reloading the privilege tables will ensure that all changes made so far
  will take effect immediately.
  
  Reload privilege tables now? [Y/n] y
  ... Success!
  
  Cleaning up...
  
  All done! If you've completed all of the above steps, your MariaDB
  installation should now be secure.
  ```

8. Test de connexion à MariaDB

```sh
sudo mariadb -u root -p
```
