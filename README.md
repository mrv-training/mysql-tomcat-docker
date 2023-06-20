## Modules
- mysql-dump: Contain initial and sample data for MySQL Database
- sample-project: Contain assets such as images, videos
- tomcat/conf: Contain configuration to run tomcat with GUI Manager and HTTPS
- tomcat/webapps: Contain sample web application
============================================================================
## Step to run
1. Install docker:
- Update the apt package index and install packages to allow apt to use a repository over HTTPS:
sudo apt-get update
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
- Add Docker’s official GPG key:
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
- Use the following command to set up the repository:
 echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
- To install the latest version, run:
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
sudo docker run hello-world

Note: If has error: "Package 'docker-ce' has no installation candidate" 
sudo snap install docker

3. Install Docker Compose: 
sudo curl -L https://github.com/docker/compose/releases/download/1.29.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
- Set the permissions:
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version

4. Use docker compose to build
docker-compose build

5. Use docker compose to run containers
docker-compose up // Run all containers
docker-compose up -d // Run all containers in background
docker-compose up -d [docker compose name] // Run all containers in background

6. Renew SSL certificates automatically by crontab:
crontab -e
30 03 01 */2 * cd /opt/docker && docker-compose up certbot

# NOTE: In the case if generating SSL certificates by certbot image fail then run certbot manually:
Install certbot
- sudo apt install certbot -y
Generate SSL certificates
- certbot certonly --standalone --email email@gmail.com -d domain-name.com -d www.domain-name.com
Use crontab to renew automatically:
crontab -e
30 03 01 */2 * certbot certonly --standalone --email email@gmail.com -d domain-name.com -d www.domain-name.com

# NOTE: If don't need HTTPS:
- Remove certbot container in docker-compose.yml file
- Remove server.xml and web.xml in folder /tomcat/conf

============================================================================
## Note
docker-compose stop [docker compose name]
docker-compose restart [docker compose name]
docker-compose down --volumes
docker rm [container name]
docker volume rm [volume name]
docker ps -a