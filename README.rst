==================================
Synapse + appservices Docker setup
==================================

This is a Docker Compose setup for development of Synapse and Matrix appservices.

Getting Started
===============
Checkout Synapse_ and the `IRC bridge appservice`_::

  $ git clone https://github.com/matrix-org/synapse.git synapse/synapse
  $ git clone https://github.com/matrix-org/matrix-appservice-irc.git irc-bridge/matrix-appservice-irc

Build the Docker images::

  $ docker-compose build

Generate keys::
  $ openssl genpkey -out irc-bridge/varlib/passkey.pem -outform PEM -algorithm RSA -pkeyopt rsa_keygen_bits:2048
  $ docker-compose run synapse python -m synapse.app.homeserver \
    -c /etc/matrix-synapse/homeserver.yaml \
    --generate-config \
    --report-stats=no \
    --server-name synapse

Generate the appservice registration file for the IRC bridge [1]_::

  $ docker-compose run appservice-irc ./bin/matrix-appservice-irc \
    --generate-registration \
    --url http://appservice-irc:9009 \
    --localpart appservice-irc \
    --config /etc/matrix-appservice-irc/config.yaml \
    --file /etc/synapse-appservice-registrations/irc.yaml

Register a Matrix user::

  $ docker up synapse # Run in a separate terminal
  $ docker-compose run synapse \
    register_new_matrix_user \
    -c /etc/matrix-synapse/homeserver.yaml \
    http://synapse:8008

Follow the prompts and then interrupt (`Ctrl+C`) the `docker up` process.

Start the Docker Compose services (you may want to do this in a separate terminal)::

  $ docker-compose up

Now point your client at `https://localhost:8008`.

.. _Synapse: https://github.com/matrix-org/synapse
.. _`IRC bridge appservice`: https://github.com/matrix-org/matrix-appservice-irc
.. [1] The appservice registration file is generated from the appservice configuration file, which is why this is not kept under version control.
