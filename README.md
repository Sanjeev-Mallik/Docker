## TO conect Mysql from PHP
docker.for.mac.host.internal

## Start Docker
docker start $(docker ps -a -q -f status=exited) 
## Create Docker Network
docker network create --driver bridge webserver 
## Install Mysql 
docker run --name mysql  -p 3306:3306  -e MYSQL_ROOT_PASSWORD=root -d mysql:8.0 

## Docker MySQL to Network

docker network connect webserver mysql
## Install PHP 8.0
Cd  80 

docker build -t suitecrm8 .  --rm 

## Image 
docker run --name "SuiteCRM8" -d -e VIRTUAL_HOST=localhost --add-host="localhost:127.0.0.1" -p 80:80 -v /Users/sanjeevmallik/Public/projects/logs/:/var/log/apache2 -v /Users/sanjeevmallik/Public/projects/SuiteCRM:/var/www/html --net webserver
