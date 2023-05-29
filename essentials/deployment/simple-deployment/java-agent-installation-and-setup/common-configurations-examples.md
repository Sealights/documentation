# Common configurations examples

We have gathered a list of the most common configurations for you

## Java CLI&#x20;

Setuping the Java Agent is possible for various configurations according to the deployment model of your Application Under Test.

When starting your application under test using a CLI command, you'll update it from&#x20;

```sh
java -jar my_app.jar
```

to

```sh
java -javaagent:/sealights/sl-cd-agent.jar \
    -Dsl.token=${SL_TOKEN}
    -Dsl.appName=microservices_orders \ 
    -Dsl.buildName=weaveworksdemos/carts:0.4.8 \
    -Dsl.tags=JRE \
    -Dsl.labId=integ_test_microservices \
    -Dsl.includes=works* \
    -jar my_app.jar
```

In some environments, the startup is deeply nested in scripts and the command line is not accessible to start the application with the necessary command-line options. In these environments, the environment variable can be useful to augment a command line as it allows you to specify the initialization of tools, specifically the launching of agents using the `-javaagent` options.

Most common variables are JAVA\_OPTS, JAVA\_OPTIONS and JAVA\_TOOL\_OPTIONS. For example:

```bash
export SEALIGHTS_OPTIONS="-javaagent:/sealights/sl-cd-agent.jar -Dsl.tokenFile=/sealights/sltoken.txt -Dsl.appName=microservices_orders -Dsl.buildName=weaveworksdemos/carts:0.4.8 -Dsl.tags=bash -Dsl.labId=integ_test_microservices -Dsl.includes=works*"
export JAVA_OPTS+="$SEALIGHTS_OPTIONS"
```

{% hint style="warning" %}
* Setting the `JAVA_TOOL_OPTIONS` will affect every JVM that runs on the machine. If you want to only have our agent run with a specific JVM, then you shouldn't use this option and prefer a more specific environment variable like JAVA\_OPTS, JAVA\_OPTIONS etc...
* JAVA\_TOOL\_OPTIONS is limited to 1024 characters and adding parameters above this buffer size will cause java to ignore it completely.
{% endhint %}

## Tomcat

The `CATALINA_OPTS` environment variable is used to pass configuration flags and system properties to the JVM that runs specifically the Tomcat server.&#x20;

```bash
SEALIGHTS_OPTIONS="-javaagent:/sealights/sl-cd-agent.jar -Dsl.tokenFile=/sealights/sltoken.txt -Dsl.appName=microservices_orders -Dsl.buildName=weaveworksdemos/carts:0.4.8 -Dsl.tags=tomcat -Dsl.labId=integ_test_microservices -Dsl.includes=works*"
CATALINA_OPTS+="$SEALIGHTS_OPTIONS"
```

{% hint style="warning" %}
Since Sealights Agent is usually in use only by Tomcat, you'll be best advised to use the`CATALINA_OPTS` variable, whereas if you put your settings in `JAVA_OPTS`, it will be used locally by other Java applications as well. \
Both options are compatible with Sealights.
{% endhint %}

If you are running Tomcat from the command line, you can just set the environment variable, either from the command line or by updating the `setenv.sh` (or `setenv.bat` in windows)

{% hint style="info" %}
Tomcat recommends using a `setenv` script to specify environment variables. You can learn more about the `setenv` script, including how to find or create it as needed, by consulting `RUNNING.txt`, which is included with every distribution of Tomcat.
{% endhint %}

### Tomcat as a Service

{% tabs %}
{% tab title="Linux" %}
If you are running Tomcat as a service on Linux, you will need to update the service file itself under `/etc/init.d` or any other startup script you have set up for the service.\


Another option is to update the `setenv.sh` (`setenv.bat` on Windows) and update the JVM parameters inside it.
{% endtab %}

{% tab title="Windows" %}
There are three ways to configure your application when running as a Windows Service:

1. Start `Tomcat9` with `//MS//`_ServiceName_ to get an icon in the system tray which gives you quick access to the configuration of the service.
2. Open the service manager in the "Control Panel". There is an entry for Tomcat. In the editor, there is a tab where you can add additional JVM parameters (See screenshot below)\
   <img src="../../../../.gitbook/assets/image (25).png" alt="" data-size="original">
3. Write a script that edits the config for you using a command like `tomcat9 //US//...` . This way, you can save the config somewhere for backup or update dynamically your server from a CI/CD script. \
   You can refer to the [official Tomcat documentation page](https://tomcat.apache.org/tomcat-9.0-doc/windows-service-howto.html#Updating\_services) for more details and options. For example, the command may look like \
   `tomcat9 //US//MyService --JvmOptions='-javaagent:/sealights/sl-cd-agent.jar -Dsl.tags=tomcat -Dsl.labId=<lab ID> [...]'`
{% endtab %}
{% endtabs %}

## Docker/Container

Below are two ways of configuring the Java agent with Dockers: by customizing the DockerFile or via Docker Compose environment setup.

### DockerFile

The container image contains the Sealights agent by default.

```docker
FROM gradle:7.6.0-jdk11-alpine AS gradle
COPY ./src src/
COPY ./settings.gradle settings.gradle
COPY ./build.gradle build.gradle
RUN gradle clean build

FROM amazoncorretto:11-alpine-jdk
RUN mkdir /opt/app
WORKDIR /opt/app
# Copy built spring application
COPY --from=gradle /home/gradle/build/libs/calculator-0.0.1-SNAPSHOT.jar ./calculator.jar
# Download the agent - it should be copied to separate image and used with Docker's "FROM" command
RUN wget -nv  https://agents.sealights.co/sl-cd-agent/sl-cd-agent-latest.zip
RUN unzip -oq sl-cd-agent-latest.zip
RUN echo "Sealights CD Agent version used is: $(cat version.txt)"
# Copy run script
COPY --chmod=777 ./scripts/run_app.sh run_app.sh
EXPOSE 8080
WORKDIR /opt/app
CMD ["/opt/app/run_app.sh", "calculator.jar"]
```

The entry point includes the Selaights JVM parameters to make sure it is kept active if the container is restarted

```bash
#!/bin/sh
## The variables are set environment level.
# SL_TOKEN=token
# SL_LAB_ID=a
# SL_BUILD_NAME=b
# DEBUG=-Dsl.httpDebugLog=yes
# LOGGING=-Dsl.log.toConsole=true
# PACKAGES="i0.sealights.demo.calculator*"

java -Dsl.log.level=DEBUG "$DEBUG $LOGGING" \
  -Dsl.workspace=. \
  -Dsl.tags=$1,cdagent,container \
  -Dsl.includes="$PACKAGES" \
  -Dsl.token="$SL_TOKEN" \
  -Dsl.labId="$SL_LAB_ID" \
  -Dsl.buildName="$SL_BUILD_NAME" \
  -Dsl.appName="$CALC_APPNAME" \
  -javaagent:./sl-cd-agent.jar \
  -jar $1
```

### Docker Compose

Typically, you can set up the agent specifically for your testing environment, by mounting the folder containing the agent, and its token, and injecting it as a `-javaagent` via the environment variables defined globally.

```yaml
queue-master:
    image: weaveworksdemos/queue-master:0.3.1
    hostname: queue-master
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    restart: always
    cap_drop:
      - all
    cap_add:
      - NET_BIND_SERVICE
    read_only: true
    tmpfs:
      - /tmp:rw,noexec,nosuid
    environment:
      - JAVA_OPTS=-javaagent:/sealights/sl-cd-agent.jar -Dsl.tokenFile=/sealights/sltoken.txt -Dsl.appName=microservices_queuemaster -Dsl.buildName=${BUILD_NAME} -Dsl.tags=script,container -Dsl.labId=integ_test_microservices -Dsl.includes=works*
    volumes:
      - /tmp/sealights:/sealights
```

A sample to use `${BUILD_NAME}` dynamically is to set it in the `.env` file:

```sh
BUILD_NAME=weaveworksdemos/queue-master:0.3.1
```

## Kubernetes

In the sample YAML file below, the agent is downloaded to a specific folder (`/download/sl-cd-agent.jar`) **mounted** to the K8s container in a dedicated volume (`/sealights`). The agent is then enabled via the `JVM_TOOLS_OPTIONS` variable set specifically for this configuration & environment ensuring the default configuration of the container is not modified.

```yaml
apiVersion: apps/v1
kind: Deployment
[...]
    spec:
      initContainers:
      - name: java-cd-agent
        image: java-cd-agent:latest
        imagePullPolicy: Never
        command: ["/bin/sh", "-c", "cp /download/sl-cd-agent.jar /sealights"]
        volumeMounts:
          - mountPath: /sealights
            name: java-cd-agent-file
      containers:
      - name: carts
        image: weaveworksdemos/carts:0.4.8
        env:
        - name: sl.token
          valueFrom:
            secretKeyRef:
              name: sealights
              key: SL_TOKEN
        - name: sl.appName
          value: microservices_carts
        - name: sl.buildName
          value: ${BUILD_NAME}
        - name: sl.tags
          value: k8s,ic
        - name: sl.labId
          value: integ_test_microservices
        - name: sl.includes
          value: works*
        - name: JAVA_TOOL_OPTIONS
          value: -javaagent:/sealights/sl-cd-agent.jar
        - name: JAVA_OPTS
          value: -Xms64m -Xmx128m -XX:+UseG1GC -Djava.security.egd=file:/dev/urandom -Dspring.zipkin.enabled=false
[...]
        volumeMounts:
        - mountPath: /tmp
          name: tmp-volume
        - mountPath: /sealights
          name: java-cd-agent-file
      volumes:
      - name: tmp-volume
        emptyDir:
          medium: Memory
      - name: java-cd-agent-file
        emptyDir: {}
[...]
```

A sample to use `${BUILD_NAME}` dynamically is to set it using `envsubst`

```sh
export BUILD_NAME=weaveworksdemos/carts:0.4.8
envsubst < k8s.yaml | kubectl apply -f -
```

Docker file for `java-cd-agent`

```docker
FROM alpine:3.17.0
ADD sl-cd-agent.jar /download/sl-cd-agent.jar
```

## JBoss/Wildfly

When the application server is JBoss or WildFly, you should also update the following parameters: `jboss.modules.system.pkgs=org.jboss.byteman,io.sealights`

```sh
SEALIGHTS_OPTIONS="-javaagent:/sealights/sl-cd-agent.jar -Dsl.tokenFile=/sealights/sltoken.txt -Dsl.appName=microservices_orders -Dsl.buildName=weaveworksdemos/carts:0.4.8 -Dsl.tags=jboss -Dsl.labId=integ_test_microservices -Dsl.includes=works*"
JAVA_OPTS+="$SEALIGHTS_OPTIONS -Djboss.modules.system.pkgs=org.jboss.byteman,io.sealights"
```

## Websphere

In the admin console:

* Go to **Servers→Application servers**
* Select your server
* Go to **Configuration→Service Infrastructure→Java and Process Management→Process Definition→Additional Properties→Java Virtual Machine**
* Add the agent configurations in the **Generic JVM arguments**&#x20;

```sh
-javaagent:/sealights/sl-cd-agent.jar -Dsl.tokenFile=/sealights/sltoken.txt -Dsl.appName=microservices_orders -Dsl.buildName=weaveworksdemos/carts:0.4.8 -Dsl.tags=websphere -Dsl.labId=integ_test_microservices -Dsl.includes=works*
```

## Weblogic

In the admin console:

* Go to **Environments→Servers**
* Select your server
* Go to **Server Start**
* Add the agent configurations in the **Arguments**&#x20;

```sh
-javaagent:/sealights/sl-cd-agent.jar -Dsl.tokenFile=/sealights/sltoken.txt -Dsl.appName=microservices_orders -Dsl.buildName=weaveworksdemos/carts:0.4.8 -Dsl.tags=weblogic -Dsl.labId=integ_test_microservices -Dsl.includes=works*
```
