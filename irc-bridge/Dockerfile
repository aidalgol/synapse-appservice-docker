FROM node:6

COPY matrix-appservice-irc/package.json /tmp/package.json
RUN cd /tmp && npm install

RUN mkdir /opt/app && cp -a /tmp/node_modules /opt/app/
COPY matrix-appservice-irc /opt/app

WORKDIR /opt/app/
CMD ["node", "--inspect=0.0.0.0:9229", "app.js", \
     "--port", "9009", \
     "--config", "/etc/matrix-appservice-irc/config.yaml", \
     "--file", "/etc/synapse-appservice-registrations/irc.yaml"]
