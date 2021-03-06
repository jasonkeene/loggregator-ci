
# Supported tags and respective `Dockerfile` links

- `latest` [(Dockerfile)][latest-dockerfile]

# Usage

- You must tell the agent where to find the routers via the `ROUTER_ADDR`
  environment variable.
- You must provide TLS certificates and keys for the agent via a volume mount.

For example:

```bash
docker run \
    --detach \
    --env "ROUTER_ADDR=router:8082" \
    --volume "$PWD/loggregator-certs:/srv/certs:ro" \
    loggregator/agent
```

[latest-dockerfile]: https://github.com/cloudfoundry/loggregator-ci/blob/master/docker-images/agent/Dockerfile
