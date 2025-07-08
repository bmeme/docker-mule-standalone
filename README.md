[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)](https://GitHub.com/Naereen/StrapDown.js/graphs/commit-activity)
[![MIT license](https://img.shields.io/badge/License-MIT-blue.svg)](https://lbesson.mit-license.org/)

Mule Standalone Packaged by Bmeme
=========

Mule Standalone docker images based on [official Eclipse Temurin repository](https://hub.docker.com/_/eclipse-temurin/), 
currently used by Bmeme for Mule-based solutions.

## What is contained in the images
* Mule, of course
* Eclipse Temurin openjdk

## Supported tags and respective `Dockerfile` links
- `4.6.3-17`, `latest`, [Dockerfile](https://github.com/bmeme/docker-mule-standalone/blob/main/4.6.3/17/Dockerfile)
- `4.6.3-11`, [Dockerfile](https://github.com/bmeme/docker-mule-standalone/blob/main/4.6.3/11/Dockerfile)
- `4.5.0-11`, [Dockerfile](https://github.com/bmeme/docker-mule-standalone/blob/main/4.5.0/11/Dockerfile)
- `4.5.0-8`, [Dockerfile](https://github.com/bmeme/docker-mule-standalone/blob/main/4.5.0/8/Dockerfile)
- `4.4.0-11`, [Dockerfile](https://github.com/bmeme/docker-mule-standalone/blob/main/4.4.0/11/Dockerfile)
- `4.4.0-8`, [Dockerfile](https://github.com/bmeme/docker-mule-standalone/blob/main/4.4.0/8/Dockerfile)

## Tag system
The tag of each image is composed by two values, separated by a `-`. 
The first one represents the Mule Standalone version. The second one represents the
OpenJDK version.

## How to use this image
### Manually
Starting your Mule standalone environment is really simple:
```shell
$ docker run --name mymulecontainer \
    -v $DOMAINS_VOLUME_PATH:/opt/mule/domains \
    -v $APP_VOLUME_PATH:/opt/mule/apps \
    -v $RESOURCES_VOLUME_PATH:/opt/mule/resources \
    -p 8081:8081 -d bmeme/mule-standalone:latest
```
where:
- **$DOMAINS_VOLUME_PATH** represents the volume path of your Mule domain(s)
- **$APP_VOLUME_PATH** represents the volume path of your Mule apps
- **$RESOURCES_VOLUME_PATH** represents the volume path of your Mule app resource(s)

### Using a Dockerfile
```dockerfile
FROM bmeme/mule-standalone:latest

COPY /path/to/domains /opt/mule/domains
COPY /path/to/apps /opt/mule/apps
COPY /path/to/resources /opt/mule/resources
```

Then, run the commands to build and run the Docker image:
```shell
$ docker build -t mymuleimage:latest .
$ docker run -d --name mymulecontainer mymuleimage:latest
```

### Using `docker-compose`
```yaml
services:
  mule:
    image: bmeme/mule-standalone:latest
    ports:
      - 8081:8081
    volumes:
      - "/path/to/domains:/opt/mule/apps"
      - "/path/to/apps:/opt/mule/domains"
      - "/path/to/resources:/opt/mule/resources"
```

## Credits
This project is a contribution of [Bmeme :: The Digital Factory](http://www.bmeme.com).
This image is actually maintained by [Daniele Piaggesi](https://github.com/g0blin79) and
[Roberto Mariani](https://github.com/jean-louis).
Any other contribution will be really appreciated.