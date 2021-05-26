# Test the application locally

## Prerequisites

- Having completed lab [03 - Fork and clone the application repo](../labs/03-Fork_and_clone_the_application_repo/README.md)
- Maven 3.x installed and ``mvn`` command in the PATH variable 
- JDK 11 installed and ``java`` command in the PATH variable 

## Run the application

Navigate your filesystem to the directory where you cloned the application's source code as required in the lab [03 - Fork and clone the application repo](../labs/03-Fork_and_clone_the_application_repo/README.md).

To run the application locally, checkout master branch

```console
$ Already on 'master'
Your branch is up to date with 'origin/master'.
```

Package the application (output is shortened for the sake of readability)

```console
$ mvn package
[INFO] Scanning for projects...
[INFO] ------------------------------------------------------------------------
[INFO] Detecting the operating system and CPU architecture
[INFO] ------------------------------------------------------------------------
[INFO] os.detected.name: osx
[INFO] os.detected.arch: x86_64
[INFO] os.detected.version: 10.15
[INFO] os.detected.version.major: 10
[INFO] os.detected.version.minor: 15
[INFO] os.detected.classifier: osx-x86_64
[INFO] 
[INFO] --------------------< it.sunnyvale.java:helloworld >--------------------
[INFO] Building myproject 1.0-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
...
[INFO] --- maven-jar-plugin:3.0.2:jar (default-jar) @ helloworld ---
[INFO] Building jar: /Users/denismaggiorotto/Documents/SoxelyNCFS/Sunnyvale/Eventi/CloudConf2020/repos/java-hello-world/target/helloworld.jar
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  19.171 s
[INFO] Finished at: 2020-11-03T00:11:28+01:00
[INFO] ------------------------------------------------------------------------
```

Set the required environment variables:

```console
$ export ENVIRONMENT=local
$ export VERSION=snapshot
```

Run the application:

```console
$ java -cp "./target/libs/*:target/*" it.sunnyvale.java.helloworld.Main
2020.11.03 00:16:34 INFO io.helidon.common.HelidonFeatures Thread[features-thread,5,main]: Helidon SE 2.1.0 features: [Config, Health, Metrics, WebServer]
2020.11.03 00:16:34 INFO io.helidon.webserver.NettyWebServer Thread[nioEventLoopGroup-2-1,10,main]: Channel '@default' started: [id: 0xf079d08c, L:/0:0:0:0:0:0:0:0:8102]
WEB server is up! http://localhost:8102/greet
```


Test the application. In another terminal, type the command:

```console
$ curl http://localhost:8102/greet
{"message":" World v.snapshot from host <YOUR PC NAME>! I'm running in local!"}
```

If the application responds as showed here after, everything is ok.