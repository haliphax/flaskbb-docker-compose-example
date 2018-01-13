# FlaskBB docker-compose example

This is an example `docker-compose` configuration for running
[FlaskBB](https://github.com/sh4nks/flaskbb/) and
[redis:alpine](https://hub.docker.com/r/library/redis/tags/alpine/) together.

Your configuration should set all of the `REDIS_*` settings to
`redis://redis:6379` and the `CACHE_REDIS_HOST` setting to `redis`.

To spin up a new installation of FlaskBB:

````
docker run -ti --rm \
	-v $(pwd)/data:/app/data \
	-v $(pwd)/config:/app/config \
	haliphax/flaskbb:latest \
	/bin/ash -c "flaskbb --config=config/flaskbb.cfg install"
````

To upgrade (while your `docker-compose` instance of FlaskBB is running):

````
docker exec -ti <web container name> \
	/bin/ash -c "flaskbb --config=config/flaskbb.cfg db upgrade"
docker-compose restart
````

Your web container name will be something like **myforum_web_1**.

**Note:** If you don't want to run FlaskBB on port 80, modify the `ports`
section of the `docker-compose.yml` file.
