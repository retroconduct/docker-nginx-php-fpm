docker pull nginx:latest
docker pull php:5.6-fpm

# remove all containers
docker rm $(docker ps -a -q)

# start php fpm
docker run --name stackphp -v /home/chathushka/workspace/docker/html/:/srv/http:ro -p 9000:9000 -d php:5.6-fpm

# start nginx 
docker run --name stacknginx -v /home/chathushka/workspace/docker/config/nginx.conf:/etc/nginx/nginx.conf -v /home/chathushka/workspace/docker/html/:/usr/share/nginx/html:ro --link stackphp:stackphp -p 80:80 -p 443:443 -d nginx:latest