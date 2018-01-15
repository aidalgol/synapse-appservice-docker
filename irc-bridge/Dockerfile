FROM node:6

ENV appdir /usr/local/src/matrix-appservice-irc/

COPY matrix-appservice-irc ${appdir}
WORKDIR ${appdir}
RUN npm install

CMD ["node", "app.js", \
     "--port", "9009", \
     "--config", "/etc/matrix-appservice-irc/config.yaml", \
     "--file", "/etc/synapse-appservice-registrations/irc.yaml"]
