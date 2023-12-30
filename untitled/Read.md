# Docker

December 13, 2023

*Outils open-source écrit dans le langage Go, créé en 2012 par trois ingénieurs français.*

C’est un outil qui peut empaqueter une application et ses dépendances dans un conteneur isolé, qui pourra être exécuté sur n'importe quel environnement.

## Avantages :

- **Réduire sur l’utilisation des ressources du système**


- **Reproductibilité du conteneur**
    - Il garantit que la bonne version de chaque dépendance soit installé.
    - Ainsi, chaque membre d'une équipe est certain d'avoir le ou les applications qui fonctionnent identiquement sur des environnements différents

- **Isolation de chaque conteneur**
    - Chaque conteneur possède ses dépendances

- **Mises à jour et tests**
    - Avec Docker, la mise à jour d'un environnement dans le cloud, même sur de nombreux serveurs est très simple.
    - Gain de temps
    - Gestion de plusieurs environnement : par exemple le classique development / tests, staging et production

- **Bonnes pratiques grâce aux images open source**
    - Des images Docker Officielles

## L’écosystème docker :

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/fcab9c97-c59c-44b8-b7a4-850b03937dde/bb19db24-9dc5-4a5f-b74c-71de1a89233e/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/fcab9c97-c59c-44b8-b7a4-850b03937dde/8175f7d5-94ce-4f5c-9734-e8b1ae2f9d0c/Untitled.png)

<aside>
<img src="/icons/reorder_gray.svg" alt="/icons/reorder_gray.svg" width="40px" /> **Lister**

```bash

# Pour lister tous les conteneurs, 
# y compris ceux qui sont seulement créés
# ou qui ne sont plus en cours d'exécution (exited). 
# Il faut utiliser l'option -a ou --all.

# Images 
docker images ls

## ou

docker images -a

# Container
docker container ls

## ou

docker ps -a
```

</aside>

<aside>
<img src="/icons/clear_red.svg" alt="/icons/clear_red.svg" width="40px" /> Supprimer

### Container

```bash
# Container arrêté
docker container rm NOM_OU_ID

# Container en cours d'éxécution
docker container rm -f redis

# Tous les conteneurs arrêté
docker container prune
```

### Images

```bash
# Image arrêté
docker image rm NOM_OU_ID

# Plusieurs Images
docker image rm alpine nginx

# Image en cours d'éxécution
docker image rm -f redis

# Toutes les images
docker image prune

```

### Tout supprimer

```bash
docker system prune
```

</aside>

## Les conteneurs :

Ils permettent d’isoler les applications pour assurer une réplicabilité des environnements

Les principes des **conteneurs Docker** sont les suivants :

- **ils sont flexibles :**
  n'importe quelle applications, même les plus complexes, peuvent être containerisée (on dit aussi "dockerisée").
- **ils sont légers :**
  le fait qu'ils partagent les ressources et le noyau Linux du système d'exploitation de la machine hôte font qu'ils sont beaucoup plus légers que des machines virtuelles (nous l'étudierons en détails dans le chapitre).
- **ils sont portables :**
  ils sont utilisables sur n'importe quel environnement (tout OS, aussi bien pour le développement local que sur des centaines de serveurs dans le cloud).
- **ils ont un couplage faible :**
  cela signifie que les conteneurs sont autonomes car ils sont isolés. Il est facile de les supprimer, les ajouter, les modifier (mise à jour par exemple) sans perturber les autres conteneurs tournant sur une machine.
- **ils sont scalables :**
  des outils permettent de déployer des centaines voir des milliers de conteneurs en quelques minutes voir secondes sur un très grande nombre de serveurs. Il est même possible d'automatiser le déploiement de nouveaux conteneurs (auto-scaling).
- **ils sont sécurisés :**
  les contraintes et l'isolation par défaut des conteneurs apporte une grande sécurité des environnements déployés.

December 14, 2023

SANS DOCKER

Architecture VM :

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/fcab9c97-c59c-44b8-b7a4-850b03937dde/065665e1-363f-41a9-a9c7-acdeecb7f362/Untitled.png)

**AVEC DOCKER**

Architecture docker :

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/fcab9c97-c59c-44b8-b7a4-850b03937dde/3a47a7ae-8044-48d0-ae36-704b88542fac/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/fcab9c97-c59c-44b8-b7a4-850b03937dde/10fa70f4-c0d0-4b46-b86a-c2a3f8c95f01/Untitled.png)

## Cycle de vie d’un conteneur :

### Crée un conteneur sans l’exécuter

```bash
docker container create alpine
```

```bash
## Créer un conteneur alpine1 et le rattaché a alpine
docker container create --name alpine1 -it  alpine
```

### Éxécuté un conteneur avec docker container start

```bash
docker container start -a alpine1
```

<aside>
<img src="/icons/warning_yellow.svg" alt="/icons/warning_yellow.svg" width="40px" /> Un conteneur non créé avec l’option -it ne peut pas être attaché a un terminal

Si la commande suivante est éxécuté

```bash
docker container create --name alpine2  alpine
```

la commande suivante ne fonctionnera pas :

```bash
docker container start -ai alpine2
```

Car le container n’est pas crée en mode interactif comme ci-dessous

```bash
docker container create --name alpine2 -it alpine
```

</aside>

<aside>
<img src="/icons/tag_blue.svg" alt="/icons/tag_blue.svg" width="40px" /> **docker start -ai**

revient a utiliser les commandes suivantes :

```bash
docker start alpine1
docker attach alpine1
```

</aside>

### Stopper un conteneur en cours d’éxécution avec docker container stop

```bash
docker container logs suspicious_brahmagupta
```

### Stopper un conteneur avec un SIGTERM

```bash
docker container stop suspicious_brahmagupta
```

### Stopper un conteneur avec un SIGKILL

```bash
docker container kill 11c5
```

### Stopper tous les conteneurs en cours d'exécution

```bash
docker stop $(docker ps -aq)
```

## État d’un conteneur

<aside>
<img src="/icons/pencil_blue.svg" alt="/icons/pencil_blue.svg" width="40px" /> **Renommer un conteneur**

```bash
docker container rename CONTENEUR NOUVEAU_NOM
```

</aside>

<aside>
<img src="/icons/playback-pause_gray.svg" alt="/icons/playback-pause_gray.svg" width="40px" /> **Mettre en pause les processus dans d'un conteneur**

```bash
docker container pause 
```

</aside>

<aside>
<img src="/icons/playback-play_gray.svg" alt="/icons/playback-play_gray.svg" width="40px" /> R**eprendre les processus dans d'un conteneur**

```bash
docker container unpause
```

</aside>

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/fcab9c97-c59c-44b8-b7a4-850b03937dde/31aeed17-ae58-4f4b-9d33-6c06f071a308/Untitled.png)

## Action dans un conteneur

<aside>
<img src="/icons/playback-play_gray.svg" alt="/icons/playback-play_gray.svg" width="40px" /> **Exécuter des commandes dans des conteneurs en cours d'exécution**

```bash
docker exec -it redis redis-cli
```

```bash
set cle 42
get cle
```

</aside>

<aside>
<img src="/icons/map-pin_gray.svg" alt="/icons/map-pin_gray.svg" width="40px" /> **Copier des fichiers et inspecter un conteneur**

```bash
docker cp SOURCE DESTINATION
```

**Conteneur vers hôte**

```bash
docker container cp test:app/log.txt  .
```

**Hôte vers conteneur**

```bash
docker cp ./test conteneur1:/home/jean
```

</aside>

<aside>
<img src="/icons/map-pin_gray.svg" alt="/icons/map-pin_gray.svg" width="40px" /> **Inspecter les changements dans le système de fichiers d'un conteneur**

```bash
docker container diff CONTENEUR
```

</aside>

<aside>
<img src="/icons/map-pin_gray.svg" alt="/icons/map-pin_gray.svg" width="40px" /> **Inspecter les processus dans un conteneur en cours d'exécution**

```bash
docker container top redis
```

</aside>

<aside>
<img src="/icons/map-pin_gray.svg" alt="/icons/map-pin_gray.svg" width="40px" /> Obtenir toutes les options de configuration d'un conteneur

```bash
docker container inspect CONTENEUR
```

</aside>

<aside>
<img src="/icons/map-pin_gray.svg" alt="/icons/map-pin_gray.svg" width="40px" /> **Visualiser l'utilisation des ressources par les conteneurs**

```bash
docker container stats
```

</aside>

<aside>
<img src="/icons/map-pin_gray.svg" alt="/icons/map-pin_gray.svg" width="40px" /> **Visualiser l'espace disque utilisé**

```bash
docker system df
```

</aside>

December 18, 2023

## Dockerfile :

<aside>
<img src="/icons/map-pin_gray.svg" alt="/icons/map-pin_gray.svg" width="40px" /> 
Un Dockerfile contient les instructions permettant à Docker de construire (build) une image automatiquement
Ce fichier contient donc toutes les commandes nécessaires à la construction de l'image que vous souhaitez.

1 - Une image de base. C'est l'image à partir de laquelle vous allez effectuer les modifications pour créer votre image. Vous n'allez en effet pas créer un système d'exploitation tout seul !

2 - Les instructions. Elles sont des commandes Docker permettant de détailler toutes les modifications à apporter à l'image de base pour aboutir à votre image finale, par exemple votre application backend.

3 - L'action. C'est la commande qui est exécutée par défaut lorsque l'image sera lancée dans un conteneur.

</aside>

## Les instructions

<aside>
<img src="/icons/playback-play_gray.svg" alt="/icons/playback-play_gray.svg" width="40px" /> **FROM**
L'instruction FROM permet d'indiquer quelle est l'image parente depuis laquelle vous allez effectuer les modifications spécifiées dans vos instructions.

```powershell
FROM image@digest
```

```powershell
FROM image:tag
```

```powershell
FROM image
```

</aside>

<aside>
<img src="/icons/playback-play_gray.svg" alt="/icons/playback-play_gray.svg" width="40px" /> **RUN**
L'instruction RUN permet d'exécuter toutes les commandes spécifiées dans une nouvelle couche (layer) au-dessus de la dernière image intermédiaire puis de sauvegarder le résultat.

La forme exec utilise un tableau JSON de mots qui seront ensuite interprétés en une instruction.

Elle permet d'exécuter des commandes avec des exécutables sans utiliser nécessairement un shell.

**Forme exec**

```powershell
RUN ["executable", "param1", "param2"]
```

```powershell
RUN ["/bin/bash", "-c", "echo Bonjour !"]
```

**Forme shell**

```powershell
**RUN ["executable", "param1", "param2"]**
```

**RUN et le cache**

```powershell
RUN apt update && apt dist-upgrade -y
```

```powershell
docker build --no-cache
```

</aside>

<aside>
<img src="/icons/playback-play_gray.svg" alt="/icons/playback-play_gray.svg" width="40px" /> **ADD**
L'instruction ADD permet de copier des fichiers, des dossiers ou des fichiers distants en utilisant des URL et de les ajouter au système de fichiers de l'image
****

```powershell
ADD SOURCE... DESTINATION
```

```powershell
ADD exemple.txt /app/
```

</aside>

<aside>
<img src="/icons/playback-play_gray.svg" alt="/icons/playback-play_gray.svg" width="40px" /> **Les patterns**

```powershell
ADD package* /app/
```

</aside>

<aside>
<img src="/icons/playback-play_gray.svg" alt="/icons/playback-play_gray.svg" width="40px" /> **COPY**

L'instruction COPY permet de copier des fichiers et des dossiers et de les ajouter au système de fichiers de l'image

```powershell
COPY ./app.js /app/
```

</aside>

<aside>
<img src="/icons/playback-play_gray.svg" alt="/icons/playback-play_gray.svg" width="40px" /> **WORKDIR**

L'instruction WORKDIR permet de modifier le répertoire de travail pour toutes les instructions RUN, CMD, ENTRYPOINT, COPY et ADD.

```powershell
WORKDIR /app
```

A noter que vous pouvez utiliser des variables d'environnement :

```powershell
ENV DIR=/app
WORKDIR $DIR/back
RUN pwd
```

</aside>

<aside>
<img src="/icons/playback-play_gray.svg" alt="/icons/playback-play_gray.svg" width="40px" /> **CMD**
L'instruction CMD permet de fournir la commande exécutée par défaut pour les conteneurs lancés depuis l'image.

```powershell
CMD ["exécutable","param1","param2"]
```

```powershell
CMD commande param1 param2
```

</aside>

<aside>
<img src="/icons/playback-play_gray.svg" alt="/icons/playback-play_gray.svg" width="40px" /> **ENTRYPOINT**
L'instruction ENTRYPOINT permet de configurer un conteneur qui sera lancé comme un exécutable

```powershell
ENTRYPOINT ["exécutable", "param1", "param2"]
```

</aside>

<aside>
<img src="/icons/playback-play_gray.svg" alt="/icons/playback-play_gray.svg" width="40px" /> **Interaction entre CMD et ENTRYPOINT**

Dockerfile

```powershell
FROM alpine

RUN apk add --update nodejs

LABEL authors="dimitriaigle"

COPY ./app.js /app/

WORKDIR /app
ENTRYPOINT ["/bin/sh"]
CMD ["localhost"]
#CMD ["node", "/app/app.js"]
```

Construction de l’image:

```powershell
docker build -t test .
```

Lancement de l’image

```powershell
docker run test
```

Résultat :

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/fcab9c97-c59c-44b8-b7a4-850b03937dde/9569814e-0f8f-4b61-a581-f72c6a043d65/Untitled.png)

```powershell
docker run -it test google.fr
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/fcab9c97-c59c-44b8-b7a4-850b03937dde/88859da7-b06e-4715-943f-0ae977d9a98a/Untitled.png)

```powershell
docker run -it --entrypoint="node" test app.js
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/fcab9c97-c59c-44b8-b7a4-850b03937dde/c0ee1dc3-68ec-4c9d-97c1-7284368a4693/Untitled.png)

</aside>

<aside>
<img src="/icons/playback-play_gray.svg" alt="/icons/playback-play_gray.svg" width="40px" /> **ARG**
L'instruction ARG permet de définir des variables qui seront utilisables par l'utilisateur lançant les conteneurs.

```powershell
ARG env
```

```powershell
docker build --build-arg env=prod
```

Mettre une valeur par défault

```powershell
ARG env=dev
```

</aside>

<aside>
<img src="/icons/playback-play_gray.svg" alt="/icons/playback-play_gray.svg" width="40px" /> **ENV**
L'instruction ENV permet de définir des variables d'environnement.

```powershell
ENV CLE="Une valeur"
```

```powershell
ENV CLE1="Une valeur1"
ENV CLE2="Une valeur2"
```

Une seule instuction

```powershell
ENV CLE1="Une valeur1" CLE2="Une valeur2"
```

</aside>

<aside>
<img src="/icons/playback-play_gray.svg" alt="/icons/playback-play_gray.svg" width="40px" /> **LABEL**
L'instruction LABEL permet d'ajouter des métadonnées à une image.

```powershell
LABEL version="2.3.1"
LABEL auteur="jean@gmail.com"
```

Une seule instuction

```powershell
LABEL version="2.3.1" auteur="jean@gmail.com"
```

</aside>