What is this?
-------------

This docker compose will create an instance of synapse using postgresql as database backend. Caddy is used as reverse proxy for TLS connections.

Steps to deploy:
----------------

1. Edit config files
    - synapse/homeserver.yaml
      postgres and listeners are configured, add your hostname instead of maugerkom.org and edit other options you need
    - caddy/Caddyfile
      change maugerkom.org for your hostname
2. Build images (config files are built into the images) `docker-compose build`
3. Generate synapse keys `docker-compose run --rm -e SYNAPSE_SERVER_NAME=<HOSTNAME> -e SYNAPSE_REPORT_STATS=yes synapse generate` (replacing HOSTNAME with your hostname)
    - This will drop a message that the config file already exists and is not regenerated. This is intended.
4. Fire the stack up `docker-compose up -d`
5. Check if everything works with https://federationtester.matrix.org/

Three volumes will be generated:
* `schemas` containing the postgres data
* `data` containing the synapse keys and other data
* `caddy` containing caddy data such as SSL keys
