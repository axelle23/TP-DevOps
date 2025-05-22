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

bash
Copier
Modifier
docker-compose up --build
Il est utile pour tester l'ensemble du projet en local avant un déploiement distant.

# 🚀 Déploiement avec Ansible
Le projet est conçu pour être déployé automatiquement sur un serveur distant (ex. axelle.brosse.takima.cloud) via Ansible et GitHub Actions.

# 📁 Dossiers Ansible typiques (à ajouter si ce n’est pas fait) :
ansible/inventories/setup.yml : inventaire Ansible (liste des hôtes).

ansible/playbook.yml : liste des tâches à exécuter (copie des fichiers, installation Docker, lancement de containers...).

# ⚙️ CI/CD avec GitHub Actions
Un fichier deploy.yml dans .github/workflows/ permet de déclencher le déploiement à chaque push sur main, en :

Se connectant au serveur distant via SSH.

Transférant les fichiers.

Exécutant ansible-playbook.

# ✅ Prérequis
Java installé pour backend_api_basic

Docker & Docker Compose

Clé SSH privée dans les secrets GitHub (ID_RSA)

Serveur distant accessible (ex: axelle.brosse.takima.cloud)
