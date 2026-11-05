# Projet Pilote

## Installation

Installé sous Windows WSL (Ubuntu) grâce à Symfony

Vous êtes chez vous, ouvrez WSL et trouvez le dossier vous appartenant

        wsl
        pwd
        cd /home/votre_repertoire/
        git clone git@github.com:WebDevCF2m/SymWebappLTS.git
        cd SymWebappLTS
        composer update

### Emplacement

Chemin Linux : `/home/formaweb/SymWebappLTS`
Chemin Windows : `//wsl.localhost/Ubuntu/home/formaweb/SymWebappLTS`

### Version de l'installation sous WSL Ubuntu

- PHP 8.5.4 (avec pas mal de bibliothèques) | https://php.watch/articles/php-8-5-installation-upgrade-guide-debian-ubuntu
- Symfony 5.22.2 | https://symfony.com/download
- Composer 2.11.1 | https://getcomposer.org/download/
- Node.js 22.22.1 (sudo apt install nodejs)
- MariaDB 11.8.6
- PhpMyAdmin 5.2.3

### Version de l'installation sous Windows

- git (`//wsl.localhost/Ubuntu/home/formaweb/SymWebappLTS`)
- docker (avec `activation de WSL sur Ubuntu`)

### Vérification de l'installation

    symfony check-requirement

Ajoutez des bibliothèques et/ou changez le php.ini 

### Vérification de sécurité

    composer audit (bibliothèques)
    symfony check:security (le tout)

suivi d'un `composer update`.

## Démarrage / arrêt

    # Démarrage
    symfony server:start (la fenêtre affiche les logs) 
    # ou
    symfony serve -d

    # Arrêt
    symfony server:stop


## Installation du contrôleur

    php bin/console make:controller

Ce qui donne

```bash
php bin/console make:controller

 Choose a name for your controller class (e.g. VictoriousGnomeController):
 > PublicController

 Do you want to generate PHPUnit tests? [Experimental] (yes/no) [no]:
 >

 created: src/Controller/PublicController.php
 created: templates/public/index.html.twig
```

Changement de la page d'accueil `src/Controller/PublicController.php`

```php
<?php

namespace App\Controller;

use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Attribute\Route;

final class PublicController extends AbstractController
{
    #[Route('/', name: 'homepage')]
    public function index(): Response
    {
        return $this->render('public/index.html.twig', [
            'controller_name' => 'PublicController',
        ]);
    }
}

```

## .env

Fichier qui est envoyé sur git, le fichier en production se nommera `.env.local` et contiendra les vrais mots de passes, url et services.

Il ne sera pas donné ni à github, ni l'IA.

On va utiliser `mariadb` plutôt que `postgre`

```bash
DATABASE_URL="mysql://app:!ChangeMe!@127.0.0.1:3306/app?serverVersion=10.11.2-MariaDB&charset=utf8mb4"
# DATABASE_URL="postgresql://app:!ChangeMe!@127.0.0.1:5432/app?serverVersion=16&charset=utf8"
```

### Installation de MariaDB


Sous WSL

```bash
sudo apt update 
sudo apt install mariadb-server
sudo service mariadb start
sudo mysql
CREATE USER 'admin'@'localhost' IDENTIFIED BY 'VOTRE_MOT_DE_PASSE'; # admin : formaweb
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'localhost' WITH GRANT OPTION; 
FLUSH PRIVILEGES; 
exit;
sudo apt install phpmyadmin php-mbstring php-zip php-gd php-json php-curl
# choisissez apache2 / yes / ok / ok /ok
sudo service apache2 start
sudo ss -tulpn | grep -E ':(80|443)\b'
sudo apache2ctl configtest
sudo nano /etc/apache2/ports.conf
sudo nano /etc/apache2/sites-enabled/000-default.conf
sudo killall apache2
sudo systemctl start apache2
 
sudo systemctl status apache2
hostname -I
sudo ln -s /etc/phpmyadmin/apache.conf /etc/apache2/conf-enabled/phpmyadmin.conf 
sudo systemctl reload apache2
http://VOTRE_IP_WSL/phpmyadmin
```

## Création de la DB

Dans `.env` on mets les paramètres 

        DATABASE_URL="mysql://admin:formaweb@localhost:3306/sym_74_lts?serverVersion=11.8.6-MariaDB&charset=utf8mb4"

et puis on crée la base de donnée `sym_74_lts`:

```bash
php bin/console doctrine:database:create
```

et vous pouvez la voir dans PHPMyAdmin