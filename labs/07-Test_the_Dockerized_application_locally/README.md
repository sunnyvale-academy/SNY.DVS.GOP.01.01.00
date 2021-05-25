# Test the Dockerized application locally

## Prerequisites

- Having completed the lab [06 - Make an application feature and publish the Docker image](labs/06-Make_an_application_feature_and_publish_the_Docker_image/README.md)

## Run the Dockerized application

If everything went fine in the previous lab, you should now be able to run the application ad a Docker container. Before running the following command, please make shure you use the correct image name (mine is dennydgl1/java-hello-world:my-feature-1).

```console
$ docker run \
    -ti \
    --rm \
    -p 8102:8102 \
    -e ENVIRONMENT=local \
    dennydgl1/java-hello-world:my-feature-1
Unable to find image 'dennydgl1/java-hello-world:my-feature-1' locally
my-feature-1: Pulling from dennydgl1/java-hello-world
bb79b6b2107f: Already exists
00028440d132: Already exists
ebd07266fb43: Already exists
5a571d0a8933: Already exists
f3e14ce44e4b: Pull complete
81970f477d55: Pull complete
Digest: sha256:f98b152393ba2984cd3a7ea622db4b95859b9e33f6b772a39b56e21ac3922444
Status: Downloaded newer image for dennydgl1/java-hello-world:my-feature-1
2020.11.03 00:19:06 INFO io.helidon.common.HelidonFeatures Thread[features-thread,5,main]: Helidon SE 2.1.0 features: [Config, Health, Metrics, WebServer]
2020.11.03 00:19:07 INFO io.helidon.webserver.NettyWebServer Thread[nioEventLoopGroup-2-1,10,main]: Channel '@default' started: [id: 0x53f32a17, L:/0.0.0.0:8102]
WEB server is up! http://localhost:8102/greet
```

In another terminal, test your application's feature:

```console
$ curl http://localhost:8102/greet
{"message":"Ciao World v.my-feature-1\n from host cbb3f3d0c3d6! I'm running in local!"}%
```

Please note the following:

- The greeting is "Ciao" as I choosed when making my application feature.
- The application version is **my-feature-1** as the tag I pushed to origin.
- hostname is **cbb3f3d0c3d6** that correspond to the running continer hosting the application.