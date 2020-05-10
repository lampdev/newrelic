#### newrelic install in docker environment

You need to replace the build args in `docker-compose.yaml` with your newrelic key, daemon host and application name:

* NEWRELIC_KEY
* NEWRELIC_APP_NAME
* NEWRELIC_DAEMON_ADDRESS