# CertBot SSL with Nginx inside Docker

An Nginx Dockerfile and docker-compose setup that includes the python-certbot-nginx script which helps generating instant SSL certificates for the NGINX proxy.

## Setup

- `docker-compose.yml` file that composes the Nginx reverse proxy and all other custom Docker images
- `./nginx` directory that contains the `Dockerfile` of Nginx with a built-in CertBot installation
- `./letsencrypt` directory which acts as a volume for the Nginx image inside `docker-compose` to maintain the certificate throughout redeployments

## Usage

**Make sure to include an nginx-volume for letsencrypt as shown in the docker-compose file to maintain the ssl-certificate after a redeployment, otherwise you may get rate-limited for a week for too many re-tries**.

1. `docker-compose up -d`
2. Run `docker-compose ps` to get the name of the running Nginx container & copy it
3. Execute the Nginx docker container using bash: `docker exec -it [name_of_nginx_container] bash`
4. Run the python-certbot-nginx script including all domain names (including subdomains) that should have HTTPS: `certbot --nginx -d [domain1] -d [domain2]...` And follow the given instructions.

5. Press `Ctrl + d` to exit bash
6. Check if your SSL certificate works [here](https://www.ssllabs.com/ssltest/) and vist `https://[your_domain]`
