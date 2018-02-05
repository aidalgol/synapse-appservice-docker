FROM python:2.7

COPY synapse /opt/app/
WORKDIR /opt/app/
ENV MAKEFLAGS="-j"
RUN ./setup.py install

CMD ["python", "-m", "synapse.app.homeserver", "--config-path=/etc/matrix-synapse/homeserver.yaml"]
