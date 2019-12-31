devops-projects
===============

### About

This tool is built with Node-Red and MongoDB. Behind the curtains, InfluxDB and Grafana are collecting statistics about the projects scraped to learn about DevOps adoption in the German Industry over time.

The stack is served by Traefik running on Docker.

The Index will be updated every 30 Minutes and Projects will be kept in the Index for 10 days before they expire.

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

### Register Gitlab Runner
```
docker exec -it gitlab-runner gitlab-runner register -n --url https://gitlab.com/ --registration-token $YOURTOKEN --executor docker --docker-image "docker:latest" --docker-privileged --docker-volumes /var/run/docker.sock:/var/run/docker.sock --tag-list "docker,dind-cache" --run-untagged="true"
```