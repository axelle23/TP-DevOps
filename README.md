Ce projet représente principalement le premier TP DevOps, vous pouvez voir le deuxième et troisième TP sur le repo suivant : https://github.com/axelle23/tp-devops-correction-docker.git

# 📁 Structure du projet
Ce projet est une architecture simple de déploiement d'une API avec une interface web statique, une base de données PostgreSQL, le tout orchestré avec Docker et déployé via Ansible.

```
.
├── backend_api_basic/
├── backend_api_multitask/
├── postgres/
├── docker-compose.yml
└── README.md
```

## 📦 backend_api_basic/
Ce dossier contient une API Java basique.

Main.java : le fichier source principal de l’API.

Main.class : la version compilée de Main.java.

Dockerfile : l’image Docker pour exécuter l'API. Il compile et lance le code Java dans un container.

## 📦 backend_api_multitask/
Cette partie correspond à une API ou un microservice qui gère plusieurs tâches, incluant ici une page HTML statique affichée sur le domaine principal.

src/main/HTTP/index.html : la page d’accueil servie à l’adresse https://axelle.brosse.takima.cloud.

src/main/HTTP/Dockerfile : construit un container web léger (ex. avec NGINX ou un serveur HTTP simple) pour exposer la page HTML.

## 🐘 postgres/
Ce répertoire est destiné à la base de données PostgreSQL utilisée par les APIs.

docker-compose.yml : définit un service PostgreSQL avec les ports, utilisateurs, mots de passe, etc.

README.md : explications sur la configuration du service de base de données.

🧩 docker-compose.yml (à la racine)
Ce fichier orchestration globale Docker peut servir à lancer tous les services (backend_api_basic, backend_api_multitask, postgres) en un seul appel :

`docker-compose up --build`

Il est utile pour tester l'ensemble du projet en local avant un déploiement distant.


# DATABASE 

### 1-1	For which reason is it better to run the container with a flag -e to give the environment variables rather than put them directly in the Dockerfile?

It is better to not stock your password on a file that over people can read. If you use it in the request nobody can access it,it will be encrypted. 

# Init database

## Persist data

### 1-2	Why do we need a volume to be attached to our postgres container?
We need a volume to keep the data. If we don’t link one to the container we can lose our data once the container restart. 

### 1-3	Document your database container essentials: commands and Dockerfile.

We can create a network to link adminer to the database. 
docker network create devops-network
Create a volume to have a persistent database. 
docker volume create - - name postgres_volume


Then create the postgres_db containers: 
docker run --name postgres_db -p 5432:5432 -e  POSTGRES_PASSWORD=we4reDATA -v postgres_volume:/var/lib/postgresql/data --network devops-network abrosse/postgres_image
docker run --network devops-network –name=adminer -p 8080:8080 adminer 

# BACKEND API

## Basics

## Multistage build

### 1-4	Why do we need a multistage build? And explain each step of this dockerfile.
So, we can generate the file and then execute it with the same file. 

# Backend API 
## HTTP SERVER

## Basics

To connect to an html page you need to use the 80 port of the container.

### 1-5 Why do we need a reverse proxy?
We need a reverse proxy so that the users don’t have a direct access to the database.  

# LINK APPLICATION

## Docker-compose

### 1-6 Why is docker-compose so important?
Docker-compose is a great tool to create multiple containers at the same time. It helps us gain a lot of time and automate the process. 
### 1-7 Document docker-compose most important commands.
I think it is docker-compose up, and the – build can be quite helpful as it helps you to rebuild every image you have created. 
### 1-8 Document your docker-compose file.

## Publish

### 1-9 Document your publication commands and published images in dockerhub.
docker login
cd simple-api
docker build -t axelle23/simple-api:latest .
docker push axelle23/simple-api:latest

### 1-10 Why do we put our images into an online repo?
So that other people can access it (member of our company for instance). So, we can access it through internet and not lost it. 


# TP 2 :
# SETUP GITHUB ACTIONS

## First steps into the CI World

## Build and test your Application

Unit tests? Component tests?
Unit test verify that every code function alone, then the components test verify that the group of program is working together. 

### 2-1 What are testcontainers?
These are lighweight docker container that helps us to run test. 

## First steps into the CD World


### 2-2 For what purpose do we need to use secured variables ?

We need to use secret to protect our personal information (such as a password) 

### 2-3 Why did we put needs: build-and-test-backend on this job? Maybe try without this and you will see!
Because if we don’t have build and test the backend before running the other tests, it will automatically be false because the backend may be missing. 

### 2-4 For what purpose do we need to push docker images?
So that we can have access to them on DockerHub.

## SETUP QUALITY GATE


# TP 3 :

# Facts

### 3-1 Document your inventory and base commands

# PLAYBOOKS

## First playbook

## Advanced Playbook

## Using roles

### 3-2 Document your playbook

Deploy your App

### 3-3 Document your docker_container tasks configuration.

## Continuous Deployment

Is it really safe to deploy automatically every new image on the hub ? explain. What can I do to make it more secure?
No, it is not always safe to automatically deploy every new image from Docker Hub, especially in a production environment. The image can be not safe and compromised the security. We can’t also always control the version of the image. To make it more secure, we can use a version tag or test it before deployment. 


