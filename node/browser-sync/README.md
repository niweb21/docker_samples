Build in the node/browser-sync folder
You have to build node/base with the name niweb21/node
```
docker build -t niweb21/browser-sync .
```

Run in the web project folder
```
docker run -dt \
    -v $(pwd):/opt/code \
    -P \
    niweb21/browser-sync \
    start --no-open --server '.' --files '*.html' 'css/*.css' 'js/*.js'
```


Run in proxy mode
```
docker network create bs

docker run -dt -p 80:80 -v $(pwd):/usr/share/nginx/html nginx:1.11

docker run -dt \
    -v $(pwd):/opt/code \
    --net bs \
    -P \
    niweb21/browser-sync \
    start --no-open --proxy "myapp.local" --files '*.html' 'css/*.css' 'js/*.js'
```
