# How to run this

### Get official nginx
docker pull nginx:latest

### Get official php-fpm
docker pull php:5.6-fpm

## Method 1

### remove all containers
docker rm $(docker ps -a -q)

### start php fpm from cli
docker run --name stackphp -v /home/chathushka/workspace/docker/html/:/srv/http:ro -p 9000:9000 -d php:5.6-fpm

### start nginx cli
docker run --name stacknginx -v /home/chathushka/workspace/docker/config/nginx.conf:/etc/nginx/nginx.conf -v /home/chathushka/workspace/docker/html/:/usr/share/nginx/html:ro --link stackphp:stackphp -p 80:80 -p 443:443 -d nginx:latest

## Method 2

### remove all containers
docker rm $(docker ps -a -q)

### start from docker composer (both services will be up in order)
docker-compose up