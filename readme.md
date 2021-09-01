docker常用环境脚本

## docker安装mysql
 docker run -p 3306:3306 --name mysql -v /opt/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=AKIAJgf5V2XVXJL5TVRQ -d mysql:latest
## docker安装redis
 docker run -p 6379:6379 --name redis -v /opt/redis/redis.conf:/etc/redis/redis.conf  -v /opt/redis/data:/data -d redis redis-server /etc/redis/redis.conf --appendonly yes
 
## docker安装nginx
 docker run -d -p 80:80 -p 10010:443 --name nginx-web -v /root/nginx/www:/usr/share/nginx/html -v /root/nginx/conf/nginx.conf:/etc/nginx/nginx.conf -v /root/nginx/logs:/var/log/nginx -v /root/nginx/conf/default.conf:/etc/nginx/conf.d/default.conf -v /root/nginx/cert:/etc/nginx/cert -v /root/nginx/download:/etc/nginx/download nginx

## docker安装nacos
 docker  run --name nacos -d -p 10006:8848 --restart=always -e JVM_XMS=1024m -e JVM_XMX=1024m -e MODE=standalone -e NACOS_AUTH_ENABLE=true nacos/nacos-server

## docker安装kafka
 安装kafka需要安装zookeeper
 docker run -d --name zookeeper -p 2181:2181 -t wurstmeister/zookeeper
 docker run -d --name kafka --publish 9092:9092 --link zookeeper --env KAFKA_ZOOKEEPER_CONNECT=zookeeper:2181 --env KAFKA_ADVERTISED_HOST_NAME=127.0.0.1 --env KAFKA_ADVERTISED_PORT=9092 --volume /etc/localtime:/etc/localtime wurstmeister/kafka:latest  
 docker run -d --name kafka --publish 9092:9092 --link zookeeper --env KAFKA_ZOOKEEPER_CONNECT=zookeeper:2181 --env KAFKA_ADVERTISED_HOST_NAME=服务器ip --env KAFKA_ADVERTISED_PORT=9092 --volume /etc/localtime:/etc/localtime wurstmeister/kafka:latest  
