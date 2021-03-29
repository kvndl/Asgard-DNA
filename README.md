# Asgard DNA
By going through these steps, it assumes you have the following in place:

 - Cloudflare API token ([more info](https://developers.cloudflare.com/api/tokens/create))
 - FQDN with relevant wildcard record

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

