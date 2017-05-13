FROM niweb21/node

RUN npm install -g browser-sync

RUN mkdir /opt/code
WORKDIR /opt/code

EXPOSE 3000 3001

ENTRYPOINT ["browser-sync"]
