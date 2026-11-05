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
