<div align="center">

# OpenClassrooms - Jardin-Actuel
</div>

<p align="center">
    <img src="https://img.shields.io/badge/MariaDB-v11.7.2-blue">
    <img src="https://img.shields.io/badge/PHP-v8.5-blue">
    <img src="https://img.shields.io/badge/Symfony-v6.2-blue">
    <img src="https://img.shields.io/badge/Angular-v15.2.0-blue">
    <img src="https://img.shields.io/badge/docker--build-passing-brightgreen">
  <br><br><br>
</p>

# Prérequis
Pour démarrer cet applicatif web vous devez avoir les outils suivants:
- Docker

# Installation and démarrage
Clonez le projet pour le récupérer
``` 
git clone https://github.com/OpenClassrooms-Student-Center/Jardin-Actuel-V2.git
cd Jardin-Actuel-V2
```
Pour démarrer le projet
```
docker compose up -d
```


Le backend est reconstruit localement (`backend/Dockerfile`) : l'application de l'image officielle `2-0-0` est copiée sur une image `php:8.5-cli`. Pour appliquer une nouvelle version de PHP : `docker compose up -d --build`.
Vérification : `docker exec jardin-actuel-symfony php -v`

## Pour éteindre le projet
Assurez vous d'être dans le dossier du projet (là où se trouve le fichier docker-compose.yml)

```
docker compose down
```

## Fin de travail
Si vous ne revenez pas sur le projet, vous avez la possibilité de supprimer les fichiers et images Docker afin de récupérer la place

Attention cela supprime tous les projets Docker de votre ordinateur

```
docker system prune -a

=> tapez Y puis Entrée
```