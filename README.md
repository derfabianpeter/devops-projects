devops-projects
===============

### About

Dies ist die Datei README.md Ihres Projekts. Es hilft den Benutzern zu verstehen, was Ihr
Projekt macht, wie man es verwendet und alles andere, was sie vielleicht wissen müssen.

### Deployment
* Create your .env file: `mv .env.example .env`
* Adjust to your liking
* Run the following commands:
```
source .env
docker-machine create --driver digitalocean --digitalocean-image ubuntu-18-04-x64 --digitalocean-region fra1 --digitalocean-size s-1vcpu-2gb --digitalocean-access-token $DO_AUTH_TOKEN $BASE_DOMAIN
eval $(docker-machine env $BASE_DOMAIN)
docker-machine ssh $BASE_DOMAIN docker network create traefik-public

docker-compose pull
docker-compose up -d
```