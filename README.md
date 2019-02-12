# Docker Compose Traefik

A docker-compose configuration for running a [Traefik](https://traefik.io/) container to serve as a reverse proxy with automatic Let's Encrypt SSL certificates.

## Usage

1. Clone this repository.
2. Copy `.env.example` to `.env` and modify the variables.
3. Run `./start.sh`.

To stop the services, run `docker-compose down`.

### Traefik

Traefik is configured to check for containers on the network specified by the `TRAEFIK_NETWORK` variable, so containers that need to be accessible by Traefik will also need to run on this network. Besides that, containers are not exposed by default, so you'll need to set the `traefik.enable` label to `true` on every container that needs to be exposed by Traefik. You'll also need to add the `traefik.frontend.rule` label to specify a Host rule, like `traefik.frontend.rule="Host:example.com"`. If the container isn't exposing port 80, you'll also need to add the `traefik.port` label set to the port that the service is running on.

When a new host rule is added, a Let's Encrypt SSL certificate is automatically acquired for it. The `LETS_ENCRYPT_EMAIL` variable specifies which email to set as the notification email.
