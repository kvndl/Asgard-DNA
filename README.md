# Asgard DNA
By going through these steps, it assumes you have the following in place:

 - Cloudflare API token ([more info](https://developers.cloudflare.com/api/tokens/create))
 - FQDN with relevant wildcard record

### What's Included
When new applications/services are added, this list will dynamically update. Enjoy.
 - Databases (info)
    - PostgreSQL
    - MariaDB
    - InfluxDB
 - Application Stack (info)
    - Traefik - Dynamic Proxy
    - Adminer - Database Management
    - Portainer - Docker Management
    - Redis - Memory Caching
    - Nextcloud - Cloud/File Storage
    - Plex - Media Processor
    - Tautulli - Plex Monitoring
    - Jackett - RSS Ingestion
    - Requestrr - Chat Bot
    - Ombi - Media Requesting
    - Radarr - Movie Manager
    - Lidarr - Audio Manager
    - Sonarr - TV Manager
    - Miniflux - RSS Reader
    - Bookstack - Documentation Aggregrator
 - VPN'd Services (info)
    

### Initial Setup
Clone where you wish to assimilate Asgard:

    git clone https://github.com/sch3p/Asgard-DNA.git
    cd Asgard-DNA

Rename some files and edit to your liking -- both files explain what values should be where:

    cp htpc/.defaults-env htpc/.env && \
    cp traefik/data/default_traefik.yml traefik/data/traefik.yml

In order to retain volume information between boots, manually create the following volumes:

    docker volume create postgres 	&& \
    docker volume create influxdb 	&& \
    docker volume create redis 	&& \
    docker volume create nextcloud-www

Do the same for the networks the stack is using:

    docker network create proxy && \
    docker network create vpn

#### Optional:
Run [ctop](https://github.com/bcicen/ctop) container to monitor instances:

    docker run --rm -ti \
	    --name=ctop \
	    --volume /var/run/docker.sock:/var/run/docker.sock:ro \
	    quay.io/vektorlab/ctop:latest

### Getting Started
Now that all the setup is out of the way, run the following to start up the engines:

    docker-compose -f htpc/docker-compose.yml up -d
Assuming all environment variables are correctly set, you should instantly have a wide-range of services available to you. 

