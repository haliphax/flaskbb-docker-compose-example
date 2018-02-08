# FlaskBB docker-compose example

This is an example `docker-compose` configuration for running
[FlaskBB](https://github.com/sh4nks/flaskbb/) and
[redis:alpine](https://hub.docker.com/r/library/redis/tags/alpine/) together.
The [haliphax/flaskbb:latest](https://github.com/haliphax/flaskbb-dockerfile)
docker image is used for FlaskBB.

Your configuration should set all of the `REDIS_*` settings to
`redis://redis:6379` and the `CACHE_REDIS_URL` setting to `REDIS_URL`.

To spin up a new installation of FlaskBB:

````
docker run -ti --rm \
	-v $(pwd)/data:/app/data \
	-v $(pwd)/config:/app/config \
	haliphax/flaskbb:latest \
	/bin/ash -c "flaskbb --config=config/flaskbb.cfg install"
````

To upgrade the database (be sure to run `docker-compose restart` afterward if
your instance is running!):

````
docker run -ti --rm \
	-v $(pwd)/data:/app/data \
	-v $(pwd)/config:/app/config \
	haliphax/flaskbb:latest \
	/bin/ash -c "flaskbb --config=config/flaskbb.cfg db upgrade"
````

## Notes

- If you don't want to run FlaskBB on port 80, modify the `ports`
section of the `docker-compose.yml` file.
- If you don't want to use a custom theme, delete the corresponding line
in the `volumes` section of the `docker-compose.yml` file.
