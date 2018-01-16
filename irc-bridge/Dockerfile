FROM node:6

RUN mkdir /usr/local/src/matrix-appservice-irc
COPY matrix-appservice-irc/package.json /usr/local/src/matrix-appservice-irc/
RUN cd /usr/local/src/matrix-appservice-irc && npm install

COPY matrix-appservice-irc /usr/local/src/

WORKDIR /usr/local/src/matrix-appservice-irc
CMD ["node", "app.js", \
     "--port", "9009", \
     "--config", "/etc/matrix-appservice-irc/config.yaml", \
     "--file", "/etc/synapse-appservice-registrations/irc.yaml"]
