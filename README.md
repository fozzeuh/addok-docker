# Conteneurs Addok pour Docker

Ces images permettent de simplifier grandement la mise en place d'une instance [addok](https://github.com/addok/addok) avec les données de références diffusées par [Etalab](https://www.etalab.gouv.fr).

## Guides d'installation

Les guides suivants ont été rédigés pour un environnement Linux ou Mac. Ils peuvent être adaptés pour Windows.

### Pré-requis

* Au moins 6 Go de RAM (à froid)
* 8 Go d'espace disque disponible (hors logs)
* [Docker CE 1.13.0+](https://docs.docker.com/engine/installation/)
* [Docker Compose](https://docs.docker.com/compose/install/) (recommandé)
* `unzip` ou équivalent
* `wget` ou équivalent

### Installer une instance avec les données de la Base Adresse Nationale en ODbL

Tout d'abord placez vous dans un dossier de travail, appelez-le par exemple `ban`.

#### Télécharger les données pré-indexées

```bash
wget https://adresse.data.gouv.fr/data/geocode/ban_odbl_addok-latest.zip
```

#### Décompresser l'archive

```bash
mkdir addok-data
unzip -d addok-data ban_odbl_addok-latest.zip
```

#### Télécharger le fichier Compose

```bash
wget https://raw.githubusercontent.com/etalab/addok-docker/master/docker-compose.yml
```

#### Démarrer l'instance

Suivant votre environnement, `sudo` peut être nécessaire pour les commandes suivantes.

```bash
# Attachée au terminal
docker-compose up

# ou en arrière-plan
docker-compose up -d
```

Suivant les performances de votre machine, l'instance mettra entre 30 secondes et 2 minutes à démarrer effectivement, le temps de charger les données dans la mémoire vive.

* 90 secondes sur une VPS-SSD-3 OVH (2 vCPU, 8 Go)
* 50 secondes sur une VM EG-15 OVH (4 vCPU, 15 Go)

Par défaut l'instance écoute sur le port `7878`.

#### Tester l'instance

```bash
curl "http://localhost:7878/search?q=1+rue+de+la+paix+paris"
```
