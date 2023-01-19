# How to use environment variables in nginx config with Docker Compose?

nginx Docker image can [extract environment variables before it starts](https://github.com/docker-library/docs/tree/master/nginx#using-environment-variables-in-nginx-configuration-new-in-119), which can be leveraged to use environment variables in the nginx config, but it comes with a few caveats.

This repo demonstrates a way of setting it up with Docker Compose. The flow is:

1. Add env variables to you `nginx.conf` file.
2. Copy it to `/etc/nginx/templates/nginx.conf.template` in the container (as opposed to your normal `/etc/nginx`).
3. Set the `NGINX_ENVSUBST_OUTPUT_DIR: /etc/nginx` environment variable in `docker-compose.yml`.

This will cause the `nginx.conf.template` file to be copied to `/etc/nginx` as `nginx.conf` and the environment variables will be replaced with their values.

There is one caveat to keep in mind: using `command` property in `docker-compose.yml` seems to be disabling the extraction functionality. If you need to run a custom command to start-up nginx, you can use the Dockerfile version.

## Example

### Run

#### No Dockerfile version

```bash
docker compose up nginx-no-dockerfile
```

#### Dockerfile version

```bash
docker compose build nginx-with-dockerfile
docker compose up nginx-with-dockerfile
```

### Test

Go to http://localhost:8081/example or http://localhost:8082/example depending on the version. You should see the contents of http://example.com proxied with the use of the environment variable.
