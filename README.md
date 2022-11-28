# ft_server

19 Coding School project (42 Network)

> This is a System Administration subject. You will discover Docker and you
will set up your first web server.

## Status

Success: 100%

## How to

[Get Docker](https://docs.docker.com/get-docker/)

Build a new image using docker build:
```
docker build -t ft_server .
```
Run the image and expose port:
```
docker run --name ft_server -p 8080:80
```
Verify if running:
```
docker ps -a
```

## Usage

Docker need to be installed. Build and run the image and go to localhost address in your favorite browser.
## References

- [Get Docker](https://docs.docker.com/get-docker/)
- [Best practices for writing Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
- [Docker CLI](https://docs.docker.com/engine/reference/run/)
- [Nginx http core mdule](https://nginx.org/en/docs/http/ngx_http_core_module.html#http)
- [HTML basics](https://developer.mozilla.org/fr/docs/Learn/Getting_started_with_the_web/HTML_basics)
