# Hello Senzing Spring-boot for Java

## :warning: Obsolete

This repository has not been updated to use the RPM/DEB installation of Senzing.

## Caveat

This repository is an example of using SpringBoot with Senzing.
It is NOT intended as a REST API server;
it does not adhere to the
official [Senzing REST API](https://github.com/Senzing/senzing-rest-api-specification),
nor has it been tuned for production.

If you are looking for Senzing's official REST API and REST API server, see
[Senzing/senzing-rest-api-specification](https://github.com/Senzing/senzing-rest-api-specification) and
[Senzing/senzing-api-server](https://github.com/Senzing/senzing-api-server).

## Overview

This demonstration shows how to wrap Senzing with Spring-boot to create an HTTP API.

The resulting HTTP API is documented in
[OpenAPI.json](doc/OpenAPI.json)
and can be viewed in the
[Swagger editor](http://editor.swagger.io/?url=https://raw.githubusercontent.com/senzing/hello-senzing-springboot-java/master/doc/OpenAPI.json).

## Install and run service

These instructions will install and run the web service.

1. [Debian-based installation](doc/debian-based-installation.md) - For Ubuntu and [others](https://en.wikipedia.org/wiki/List_of_Linux_distributions#Debian-based)
1. [RPM-based installation](doc/rpm-based-installation.md) - For Red Hat, CentOS, openSuse and [others](https://en.wikipedia.org/wiki/List_of_Linux_distributions#RPM-based).

## Test

The following tests assume that the service is running.
To start and run the service, see either
[Debian-based "Run Service"](doc/debian-based-installation.md#run-service) or
[RPM-based "Run Service"](doc/rpm-based-installation.md#run-service).

### Find port

Normally the service runs on port 8080.
To verify this, the end of the service log sent to standard out (STDOUT) will have the port information.

```console
YYYY-MM-DD HH:MM:SS.sss  INFO 8032 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http) with context path ''
YYYY-MM-DD HH:MM:SS.sss  INFO 8032 --- [           main] c.s.senzingdemo.SenzingDemoApplication   : Started SenzingDemoApplication in 11.077 seconds (JVM running for 12.172)
```

### Test port

To test the service, open a web-browser (e.g. FireFox, Chrome, Safari, MS Explorer, Opera) to
`http://localhost:8080/stats`, replacing `localhost` if needed.

### Try the API

1. Set environment variables.

    ```console
    export GIT_REPOSITORY_DIR=~/senzing.git/hello-senzing-springboot-java
    export SENZING_DEMO_DATASOURCE="TEST"
    export SENZING_DEMO_URL="http://localhost:8080"
    ```

1. Get the Senzing workload statistics.

    ```console
    curl -X GET \
      ${SENZING_DEMO_URL}/stats
    ```

1. If you would like the JSON HTTP response formatted, you can pipe the output to `jq`.  Example:

    ```console
    curl -X GET \
      ${SENZING_DEMO_URL}/stats | jq
    ```

1. Exercise a number of APIs via `curl` command in [curl-command.sh](doc/curl-commands.sh).

    ```console
    cd ${GIT_REPOSITORY_DIR}/doc
    ./curl-commands.sh > curl-commands.out 2>&1
    ```

    View results in `${GIT_REPOSITORY_DIR}/doc/curl-commands.out`

## References

1. [Spring Boot](http://spring.io/projects/spring-boot)
    1. [Spring initializr](https://start.spring.io/)
