# Nginx Alpine with HTTP Redis

This repo contains latest official Docker image of [Nginx Alpine](https://hub.docker.com/_/nginx/) with [HTTP Redis](https://www.nginx.com/resources/wiki/modules/redis/) module compiled in.

Usage:

```shell
docker run -d -v ./nginx.conf:/etc/nginx/conf.d/default.conf:ro stepankuzmin/nginx-with-redis
```

Example configuration:

```nginx
server {
    location / {
        set $redis_key $uri;

        redis_pass     name:6379;
        default_type   text/html;
        error_page     404 = /fallback;
    }

    location = /fallback {
        proxy_pass backend;
    }
}
```

**Note**: The backend should set the data in redis. The redis key is `/uri?args`.
