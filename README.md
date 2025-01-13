# caddy-docker-custom

![Build Status](https://github.com/emarshal/caddy-docker-custom/actions/workflows/docker.yaml/badge.svg)

Heavily inspired by [IAreKyleW00t/docker-caddy-cloudflare](https://github.com/IAreKyleW00t/docker-caddy-cloudflare), the official [Caddy](https://github.com/caddyserver/caddy/) [Docker image](https://hub.docker.com/_/caddy) with additional modules added:
* [caddy-dns/cloudflare](https://github.com/caddy-dns/cloudflare) module for DNS-01 ACME validation support with Cloudflare.

```sh
docker pull docker.io/emarshal/caddy-custom:latest
```

## Release Notes

See [Caddy Releases](https://github.com/caddyserver/caddy/releases).

## Customization

This repository makes some opininiated choices for my particular environment/usage. Suggest reviewing at minimum, the following:

* Included modules. (In `Dockerfile`.)
* Supported platforms. (In `docker/build-push-action` step in `docker.yaml`.)

## Tags

The following tags are available for the `emarshal/caddy-custom` image.

* `latest`
* `<version>` (eg: `2.6.4`, including: `2.6`, `2`, etc.)

## Usage

Refer to the official [Caddy](https://hub.docker.com/_/caddy) Docker image and [docs](https://caddyserver.com/docs/) for more information on using Caddy.

Create the container as usual and include your `CF_API_TOKEN`. We can utilizing Caddy's support for [Environment varaiables](https://caddyserver.com/docs/caddyfile/concepts#environment-variables) to pass these values into our `Caddyfile`.

Then set the global [acme_dns](https://caddyserver.com/docs/caddyfile/options#acme-dns) directive in your `Caddyfile`

```
{
  acme_dns cloudflare {env.CF_API_TOKEN}
}
```

See the [caddy-dns/cloudflare](https://github.com/caddy-dns/cloudflare) module and [`tls`](https://caddyserver.com/docs/caddyfile/directives/tls#tls) directive for advanced usage.

### Creating a Cloudflare API Token

You can generate a Cloudflare API token via the Cloudflare web console using the following steps:

1. Login to your [Dashboard](https://dash.cloudflare.com/)
2. Go to [Account Profile](https://dash.cloudflare.com/profile) > [API Tokens](https://dash.cloudflare.com/profile/api-tokens)
3. Click "Create token" (Use the "Create Custom Token" option)
4. Grant the following permissions:
   * `Zone > Zone > Read`
   * `Zone > DNS > Edit`

## Building

You can build the Docker image locally by doing

```sh
docker build -t caddy-custom .
```
