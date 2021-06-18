# Setup

## Docker installation

Note:- don't run from root user.

````SHELL
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker $USER
````

Run this command to download the current stable release of Docker Compose:

````SHELL
sudo curl -L "https://github.com/docker/compose/releases/download/1.25.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
````
To install a different version of Compose, substitute 1.25.5 with the version of Compose you want to use.

If you have problems installing with curl, see Alternative Install Options tab above.

Apply executable permissions to the binary:

````SHELL
sudo chmod +x /usr/local/bin/docker-compose
````

Note:- To run docker-compose cd to-your-root-rpt-directory - Where docker-compose.yml file exist.

## Clone code repo

### Clone the docker-compose repository
````SHELL
git clone https://gitlab.codilar.in/devops/docker-compose-magento.git <project-name>
cd <project-name>
````

### Magento
````SHELL
git clone --branch development <paste you magento repository url> src
````

### Configure project
````SHELL
nano .application // MAGENTO_BASEURL=http://<project-name>.local  Save and close
nano deploy/nginx.conf  // server_name <project-name>.local;    Save and close
````

## First time RUN

````SHELL
docker-compose -f docker-compose.yml -f docker-compose.dev.yml up -d --build
docker-compose exec app bash
sudo nano /etc/hosts
127.0.0.1 <project-name>.local // Add the new line or udate existing one. Save and close
````

## Docker services logs

````SHELL
docker-compose logs -f // For all services
docker-compose logs -f <service-name> // For perticular service. Services names are db(MYSQL), backend(PHP-FPM log), frontend(Yarn dev log), redis(Redis log), api(Graphql Nginx log), and nginx(Proxy log for Node and Graphql) 
````

## Access from Browser

1. [http://<project-name>.local/] for Frontend

2. [http://<project-name>.local/admin] for Admin

3. [http://<project-name>.local/adminer] for Database

4. [http://<<project-name>.local:1080/maildev/] for Mail Server

5. [http://<project-name>.local:9200/] for Elasticsearch

6. [http://<project-name>.local:15672/] for RabbitMq

## Regular

````SHELL
docker-compose -f docker-compose.yml -f docker-compose.dev.yml up -d
docker-compose stop
````

## Restart Services

````SHELL
docker-compose restart // For all services
docker-compose restart <service-name> // For perticular service
````

## Recreate Services

````SHELL
docker-compose -f docker-compose.yml -f docker-compose.dev.yml up -d --force-receate
````
## Flush all Services

````SHELL
docker-compose down --remove-orphans
````


