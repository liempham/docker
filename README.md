# Docker images
For typical dev packages

## build
cd centos
docker build -t="centos7-php7-node8:latest" .

## run
docker run -d -p 80:80 -v <host_path>/www/html/:/var/www/html centos7-php7-node8:latest
