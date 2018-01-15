FROM python:2.7

ENV appdir /usr/local/src/synapse/

COPY synapse ${appdir}
WORKDIR ${appdir}
ENV MAKEFLAGS="-j"
RUN ./setup.py install

CMD ["python", "-m", "synapse.app.homeserver", "--config-path=/etc/matrix-synapse/homeserver.yaml"]
