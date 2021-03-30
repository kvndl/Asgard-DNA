# <img width="35px" src="./etc/logo.png" alt="Asgard"></img> Asgard DNA 

By going through these steps, it assumes you have the following in place:

 - Cloudflare API token [[more info](https://developers.cloudflare.com/api/tokens/create)]
 - FQDN with relevant wildcard record

### What's Included

- Fully-automated, reverse proxied, subdomain-based stack
- Media server capable of grabbing releases in a wide-range of mediums
- Cloud drive to collaborate, serve, and share files
- Database management via Adminer
- RSS ingestion (optionally) with API access
- VPN'd select services to route traffic from ISP  

Databases [[info](https://github.com/sch3p/Asgard-DNA/blob/master/README.md)]

- [PostgreSQL](https://www.postgresql.org)

- [MariaDB](https://mariadb.org/)

- [InfluxDB](https://www.influxdata.com/)

Application Stack [[info](https://github.com/sch3p/Asgard-DNA/blob/master/README.md)]
   
   - [Traefik](https://traefik.io/) - Dynamic Proxy
   
   - [Adminer](https://www.adminer.org/) - Database Management
   
   - [Portainer](https://www.portainer.io/) - Docker Management
   
   - [Redis](https://redis.io/) - Memory Store
   
   - [Nextcloud](https://nextcloud.com/) - Cloud/File Storage
   
   - [Plex](https://www.plex.tv/) - Media Processor
   
   - [Tautulli](https://tautulli.com/) - Plex Monitoring
   
   - [Requestrr](https://github.com/darkalfx/requestrr) - Chat Bot
   
   - [Ombi](https://ombi.io/) - Media Requesting
   
   - [Radarr](https://radarr.video/) - Movie Manager
   
   - [Lidarr](https://lidarr.audio/) - Audio Manager
   
   - [Sonarr](https://sonarr.tv/) - TV Manager
   
   - [Miniflux](https://miniflux.app/) - RSS Reader
   
   - [Bookstack](https://www.bookstackapp.com/) - Documentation Storage

VPN Services [[info](https://github.com/sch3p/Asgard-DNA/blob/master/README.md)]

 - [Gluetun](https://github.com/qdm12/gluetun) - OpenVPN Docker client

 - [Qbittorrent](https://www.qbittorrent.org/) - Torrent Downloader

 - [Jackett](https://github.com/Jackett/Jackett) - RSS Indexer



### Initial Setup

Clone where you wish to assimilate Asgard:

    git clone https://github.com/sch3p/Asgard-DNA.git
    cd Asgard-DNA

Ensure Docker and Docker Compose are installed on the target system [[official docs](https://docs.docker.com/compose/install/)]

- Ubuntu/Debian: `sh scripts/docker-setup/ubuntu.sh`
- CentOS/RHEL: `sh scripts/docker-setup/rhel.sh` <- WIP
- Fedora: `sh scripts/docker-setup/fedora.sh` <- WIP
- Arch: `sh scripts/docker-setup/arch.sh` <- WIP

Rename some files and edit to your liking -- both files explain what values should be where:

    cp htpc/.defaults-env htpc/.env && \
    cp traefik/data/default_traefik.yml traefik/data/traefik.yml

In order to retain volume information between boots, manually create the following volumes:

    docker volume create postgres 	&& \
    docker volume create influxdb 	&& \
    docker volume create redis 	&& \
    docker volume create nextcloud-www

Do the same for the network the stack is using:

    docker network create proxy

#### Optional:
Run [ctop](https://github.com/bcicen/ctop) container to monitor instances:

    docker run --rm -ti \
	    --name=ctop \
	    --volume /var/run/docker.sock:/var/run/docker.sock:ro \
	    quay.io/vektorlab/ctop:latest

### Getting Started
Now that all the setup is out of the way, run the following to start up the engines:

    docker-compose -f htpc/docker-compose.yml up -d

To ensure everything stood up correctly, visit Traefik's Dashboard:

    https://traefik.<<domain>.com

Each service should be available at their respective sub-domain:

    https://service.<<domain>.com

