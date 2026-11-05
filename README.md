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
- docker (avec activation de WSL sur Ubuntu)

### Vérification de l'installation

    symfony check-requirement

Ajoutez des bibliothèques et/ou changez le php.ini 

