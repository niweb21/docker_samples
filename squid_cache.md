
Ne fonctionne
Attention ADD n'est pas caché, mais même avec un curl ça fonctionne pas :'(

http://stackoverflow.com/questions/22030931/how-to-rebuild-dockerfile-quick-by-using-cache

# get squid
docker run --name squid -d \
  --publish 3128:3128 \
  --volume /srv/docker/squid/cache:/var/spool/squid3 \
  sameersbn/squid:3.3.8-23

# optionally in another terminal run tail on logs
docker exec -it squid tail -f /var/log/squid3/access.log

# get squid ip to use in docker build
SQUID=http://$(docker inspect --format '{{ .NetworkSettings.IPAddress }}' squid):3128

# build your instance
docker build --build-arg http_proxy=$SQUID https_proxy=$SQUID -t niweb21/node .
