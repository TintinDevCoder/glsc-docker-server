# glsc-docker-server


docker run \
  --name=mysql \
  --hostname=5c6d801b77c0 \
  --volume /mydata/mysql/conf:/etc/mysql/conf.d \
  --volume /mydata/mysql/data:/var/lib/mysql \
  --volume /mydata/mysql/log:/var/log/mysql \
  --env=MYSQL_ROOT_PASSWORD=root \
  --network=bridge \
  -p 3308:3306 \
  --restart=always \
  --detach=true \
  mysql:8.0 \
  --character-set-server=utf8mb4 \
  --collation-server=utf8mb4_unicode_ci





docker run \
  --name=nginx \
  --volume /mydata/nginx/conf:/etc/nginx \
  --volume /mydata/nginx/html:/usr/share/nginx/html \
  --volume /mydata/nginx/logs:/var/log/nginx \
  --network=bridge \
  -p 80:80 \
  --restart=always \
  --detach=true \
  nginx:1.10 \
  nginx -g 'daemon off;'


docker run \
  --name=kibana \
  --hostname=f6478e679c43 \
  --user=kibana \
  --env=ELASTICSEARCH_HOSTS=http://10.157.6.81:9200 \
  --network=bridge \
  -p 5601:5601 \
  --restart=always \
  --detach=true \
  kibana:7.4.2 \
  /usr/local/bin/kibana-docker




docker run \
  --name=elasticsearch \
  --volume /mydata/elasticsearch/config/elasticsearch.yml:/usr/share/elasticsearch/config/elasticsearch.yml \
  --volume /mydata/elasticsearch/data:/usr/share/elasticsearch/data \
  --volume /mydata/elasticsearch/plugins:/usr/share/elasticsearch/plugins \
  --env=discovery.type=single-node \
  --env='ES_JAVA_OPTS=-Xms64m -Xmx512m' \
  --network=bridge \
  -p 9200:9200 \
  -p 9300:9300 \
  --restart=always \
  --detach=true \
  elasticsearch:7.4.2
