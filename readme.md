# README Technique

## Prérequis

Avant de commencer, assurez-vous que vous avez les outils suivants installés sur votre machine :

* **Docker** : [Installation de Docker](https://docs.docker.com/get-docker/)
* **Docker Compose** : [Installation de Docker Compose](https://docs.docker.com/compose/install/)

## Installation des Conteneurs

1. Clonez ce repository ou téléchargez le fichier `docker-compose.yml` sur votre machine.
2. Assurez-vous que Docker est en cours d'exécution sur votre machine.

### Lancer les services avec Docker Compose

Dans le répertoire contenant le fichier `docker-compose.yml`, exécutez la commande suivante pour démarrer tous les services (PostgreSQL, MongoDB, pgAdmin, Mongo Express, et le service Python avec Jupyter) :

```bash
docker-compose up -d
```

Cela démarrera les conteneurs en arrière-plan, chacun ayant ses propres services associés :

* **PostgreSQL** (accès via le conteneur `postgres_container`)
* **pgAdmin** (accès via `http://localhost:5050`)
* **MongoDB** (accès via le conteneur `mongo_container`)
* **Mongo Express** (accès via `http://localhost:8081`)
* **Python service** avec Jupyter (accès via `http://localhost:8888`)

## Lancer un Notebook Jupyter

1. **Accédez au conteneur Python** :
   Une fois les services démarrés, vous pouvez accéder au conteneur Python pour lancer un notebook Jupyter :

   ```bash
   docker exec -it python_service_container bash
   ```
2. **Démarrez Jupyter Notebook** :
   Une fois dans le conteneur, lancez Jupyter avec la commande suivante :

   ```bash
   jupyter notebook --ip=0.0.0.0 --port=8888 --no-browser --allow-root
   ```

   Cette commande démarre le serveur Jupyter, accessible depuis votre navigateur à l'adresse suivante :

   [http://localhost:8888](http://localhost:8888/)
3. **Accéder à l'interface Jupyter** :
   Ouvrez votre navigateur et accédez à l'URL :

   [http://localhost:8888](http://localhost:8888/)
   Si un **token** est requis, copiez-le depuis le terminal où Jupyter est lancé.
4. **Placer vos Notebooks** :
   Vous pouvez maintenant placer vos notebooks Jupyter dans le répertoire du fichier docker-compose sur votre machine locale. Ils seront accessibles dans le conteneur sous le répertoire `/app`.
   Pour cela, déplacez vos fichiers `.ipynb` dans le dossier courant.
5. **Exécuter les Notebooks** :
   Depuis l'interface Jupyter dans votre navigateur, vous pouvez ouvrir et exécuter vos notebooks comme d'habitude.

---

## Arrêter les Services

Pour arrêter tous les services et conteneurs lancés par Docker Compose, utilisez la commande suivante dans le même répertoire que votre fichier `docker-compose.yml` :

```bash
docker-compose down
```

Cela arrêtera tous les conteneurs et supprimera les ressources associées (volumes, réseaux).

---

## Supprimer les Conteneurs et Volumes

Si vous souhaitez également supprimer les volumes associés (par exemple, les bases de données PostgreSQL et MongoDB), utilisez cette commande :

```bash
docker-compose down -v
```

Cela supprimera tous les volumes associés aux conteneurs et réinitialisera les bases de données.

---

## Récapitulatif des Ports

Voici un récapitulatif des ports utilisés par chaque service pour accéder aux applications :

* **PostgreSQL** : `localhost:5432`
* **pgAdmin** : `http://localhost:5050`
* **MongoDB** : `localhost:27017`
* **Mongo Express** : `http://localhost:8081`
* **Jupyter Notebook** : `http://localhost:8888`

---

## Résolution des Problèmes

### Le conteneur Python ne démarre pas

Si vous rencontrez des problèmes lors du démarrage du conteneur Python, assurez-vous que Docker est bien installé et que le fichier `docker-compose.yml` est correctement configuré. Vérifiez également que vous avez suffisamment d'espace disque disponible.

Pour obtenir des détails sur les logs du conteneur Python, vous pouvez utiliser la commande suivante :

```bash
docker logs python_service_container
```

Cela vous permettra de vérifier si des erreurs se produisent lors du démarrage du conteneur.
