---

title: "Run CadenzaFlow using Docker"
weight: 20

menu:
  main:
    name: "Docker"
    identifier: "installation-guide-docker"
    parent: "installation-guide"
    pre: "Run the Full Distribution using Docker"

---

# Community Edition

The Community Edition docker images can be found on [GitHub](https://github.com/cadenzaflow/docker-cadenzaflow-bpm-platform) and [Docker Hub](https://hub.docker.com/r/cadenzaflow/cadenzaflow-bpm-platform/).

## Start CadenzaFlow Run using Docker

To start [CadenzaFlow Run]({{< ref "/user-guide/cadenzaflow-bpm-run.md" >}}) execute the following commands:

```shell
docker pull cadenzaflow/cadenzaflow-bpm-platform:run-latest
docker run -d --name cadenzaflow -p 8080:8080 cadenzaflow/cadenzaflow-bpm-platform:run-latest
```

## Start CadenzaFlow (Tomcat) using Docker

To start CadenzaFlow, execute the following commands:

```shell
docker pull cadenzaflow/cadenzaflow-bpm-platform:latest
docker run -d --name cadenzaflow -p 8080:8080 cadenzaflow/cadenzaflow-bpm-platform:latest
```

Please note that by default the Apache Tomcat distribution is used. For a guide on how to use one of the other distributions, see the [tag schema](https://github.com/cadenzaflow/docker-cadenzaflow-bpm-platform#supported-tagsreleases).


# Enterprise Edition

{{< enterprise >}}
Please note that these docker images are offered only for CadenzaFlow Enterprise Edition.
{{< /enterprise >}}

We offer to our customers a Docker image for the Enterprise edition of CadenzaFlow.

These images are hosted on our dedicated Docker registry and are available to Enterprise customers only. You can browse the available images in our [Docker registry](https://registry.cadenzaflow.com) after logging-in with your credentials.

Please note that these images are build using the same Dockerfile of the Community image, but including the Enterprise version of CadenzaFlow. For this reason, the same [documentation](https://github.com/cadenzaflow/docker-cadenzaflow-bpm-platform#database-environment-variables) applies.

Make sure to log-in correctly before trying to pull the image:

```shell
$ docker login registry.cadenzaflow.com
Username: my.username
Password:
Login Succeeded

$ docker pull registry.cadenzaflow.com/cambpm-ee/cadenzaflow-bpm-platform-ee:{{< minor-version >}}.0
{{< minor-version >}}.0: Pulling from cadenzaflow-bpm-platform-ee
ff3a5c916c92: Already exists
5de5f69f42d7: Already exists
fa7536dd895a: Pull complete
46ce7a9973c1: Pull complete
6fa1782e4a59: Pull complete
fbf8f17dff48: Pull complete
Digest: sha256:47598932a4aff210ce91819d3b75adbfde675017b13ce9881c9d7dca682fba96
Status: Downloaded newer image for registry.cadenzaflow.com/cambpm-ee/cadenzaflow-bpm-platform-ee:{{< minor-version >}}.0
```

If you want to build an enterprise image yourself, follow the steps described on [GitHub](https://github.com/cadenzaflow/docker-cadenzaflow-bpm-platform#build-a-enterprise-version).