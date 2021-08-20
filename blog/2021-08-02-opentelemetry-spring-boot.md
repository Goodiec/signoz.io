---
title: Monitor your Spring Boot application with OpenTelemetry and SigNoz
slug: opentelemetry-spring-boot
date: 2021-08-02
tags: [application-monitoring, java-monitoring]
author: Ankit Anand
author_title: SigNoz Team
author_url: https://github.com/ankit01-oss
author_image_url: https://avatars.githubusercontent.com/u/83692067?v=4
description: End-to-end performance monitoring of Spring Boot application with OpenTelemetry. Get your telemetry data visualized with SigNoz.
image: /img/blog/2021/08/opentelemetry_springboot_hc.png
keywords:
  - OpenTelemetry
  - OpenTelemetry java
  - Spring Boot
  - OpenTelemetry Spring Boot
  - application monitoring
---

OpenTelemetry can auto-instrument your Spring Boot application to capture telemetry data from a number of popular libraries and frameworks. Let's learn how it works.

<!--truncate-->

![Cover Image](/img/blog/2021/08/opentelemetry_springboot_hc-min.png)

OpenTelemetry is a vendor-agnostic instrumentation library. In this article, let's explore how you can auto-instrument your Java Spring Boot application with OpenTelemetry and get the data reported through SigNoz - an open-source APM and observability tool.

Steps to get started with OpenTelemetry for Spring Boot application:

- Installing SigNoz
- Installing sample Spring Boot app
- Auto instrumentation with OpenTelemetry and sending data to SigNoz

## Installing SigNoz

You can get started with SigNoz using just three commands at your terminal if you have Docker installed. You can read about other deployment options from [SigNoz documentation](https://signoz.io/docs/deployment/requirement/).

    git clone https://github.com/SigNoz/signoz.git
    cd signoz/deploy/
    ./install.sh

<br></br>You will have an option to choose between ClickHouse or Kafka + Druid as a storage option. Trying out SigNoz with ClickHouse database takes less than 1.5GB of memory, and for this tutorial, we will use that option.

When you are done installing SigNoz, you can access the UI at: [http://localhost:3000](http://localhost:3000/application)

The application list shown in the dashboard is from a sample app called HOT R.O.D that comes bundled with the SigNoz installation package.

import Screenshot from "@theme/Screenshot"

<Screenshot
   alt="SigNoz dashboard showing application list"
   height={500}
   src="/img/blog/2021/08/signoz_dashboard_hc.png"
   title="SigNoz Dashboard"
   width={700}
/>

## Installing sample Spring Boot app

For this tutorial, we will use a sample Spring Boot application built using Maven. You can find the code for the application at its <a href = "https://github.com/spring-projects/spring-petclinic" rel="noopener noreferrer nofollow" target="_blank" >GitHub repo</a>.

Steps to get the app set up and running:

1. Git clone the repository and go to the root folder

   ```
   git clone https://github.com/spring-projects/spring-petclinic.git
   cd spring-petclinic
   ```

2. Update port
   This app runs on port `8080` by default. But port `8080` is used by SigNoz for its query service, so let's update the port number to something else.

   Open the `application.properties` file located at `spring-petclinic/src/main/resources` and update the server.port attribute.

   ```
   # database init, supports mysql too

   database=h2
   spring.datasource.schema=classpath*:db/${database}/schema.sql
   spring.datasource.data=classpath*:db/${database}/data.sql

   # Web

   spring.thymeleaf.mode=HTML
   server.port=8090

   # JPA

   spring.jpa.hibernate.ddl-auto=none
   spring.jpa.open-in-view=false

   # Internationalization

   spring.messages.basename=messages/messages

   # Actuator

   management.endpoints.web.exposure.include=\*

   # Logging

   logging.level.org.springframework=INFO

   # logging.level.org.springframework.web=DEBUG

   # logging.level.org.springframework.context.annotation=TRACE

   # Maximum time static resources should be cached

   spring.resources.cache.cachecontrol.max-age=12h
   ```

   Also, update the port number in [petclinic_test_plan.jmx](https://github.com/SigNoz/spring-petclinic/blob/main/src/test/jmeter/petclinic_test_plan.jmx) located at `spring-petclinic/src/test/jmeter` to `port number: 8090`. It will appear under `PETCLINIC_PORT` elementProp.

3. Run the application using the following commands.

   ```
   ./mvnw package
   java -jar target/*.jar
   ```

   You can now access the application UI here: [http://localhost:8090/](http://localhost:8080/)

<Screenshot
   alt="Spring PetClinic app accessed at port:8090"
   height={500}
   src="/img/blog/2021/08/spring_petclinic_hc.png"
   title="Sample Spring Boot application running in your local host."
   width={700}
/>

Once you ensure that your application runs fine, stop it with `ctrl + z` on mac, as we will be launching the application with the Java agent downloaded from OpenTelemetry.

## Auto instrumentation with OpenTelemetry and sending data to SigNoz

For instrumenting Java applications, OpenTelemetry has a very handy Java JAR agent that can be attached to any Java 8+ application. The JAR agent can detect a number of <a href = "https://github.com/open-telemetry/opentelemetry-java-instrumentation/blob/main/docs/supported-libraries.md" rel="noopener noreferrer nofollow" target="_blank" >popular libraries and frameworks</a> and instrument it right out of the box. You don't need to add any code for that.

1. Download the [latest Java JAR agent](https://github.com/open-telemetry/opentelemetry-java-instrumentation/releases/latest/download/opentelemetry-javaagent-all.jar).
2. Now you need to enable the instrumentation agent as well as run your sample application. You can do so by the following command:

```
OTEL_METRICS_EXPORTER=none OTEL_EXPORTER_OTLP_ENDPOINT="http://IP of SigNoz:4317" OTEL_RESOURCE_ATTRIBUTES=service.name=javaApp java -javaagent:/path/to/opentelemetry-javaagent-all.jar -jar target/\*.jar
```

<br></br>As you are running this on your local host, you need to replace `IP of SigNoz` with `localhost`. The path should be updated to where you have kept your downloaded Java JAR agent. Your final command will look like this:<br></br>

    OTEL_METRICS_EXPORTER=none OTEL_EXPORTER_OTLP_ENDPOINT="http://localhost:4317" OTEL_RESOURCE_ATTRIBUTES=service.name=javaApp java -javaagent:/Users/Downloads/opentelemetry-javaagent-all.jar -jar target/*.jar

<br></br>Note the path is updated for my local environment.

Check out the Spring Pet Clinic app at: [http://localhost:8090/](http://localhost:8090/) and play around with it to generate some load. It might take 1-2 minutes before it starts showing up in the SigNoz dashboard.

Below you can find your `javaApp` in the list of applications being monitored.

<Screenshot
   alt="`Javaapp` appears in the list of applications monitored through SigNoz"
   height={500}
   src="/img/blog/2021/08/javaapp_boxed_hc.png"
   title="`javaApp` in the list of applications monitored"
   width={700}
/>

## Metrics and Traces of the Spring Boot application

SigNoz makes it easy to visualize metrics and traces captured through OpenTelemetry instrumentation.

SigNoz comes with out of box RED metrics charts and visualization. RED metrics stands for:

- Rate of requests
- Error rate of requests
- Duration taken by requests
  <Screenshot
       alt="SigNoz dashboard showing application latency, requests per sec, error percentage and top endpoints"
       height={500}
       src="/img/blog/2021/08/signoz_charts_hc.png"
       title="Measure things like application latency, requests per sec, error percentage and see your top endpoints with SigNoz."
       width={700}
  />

You can then choose a particular timestamp where latency is high to drill down to traces around that timestamp.
<Screenshot
     alt="List of traces shown on SigNoz dashboard"
     height={500}
     src="/img/blog/2021/08/signoz_visualization_hc.png"
     title="View of traces at a particular timestamp"
     width={700}
/>

You can use flamegraphs to exactly identify the issue causing the latency.

<Screenshot
     alt="Flamegraphs and gantt charts to visualize time taken by requests"
     height={500}
     src="/img/blog/2021/08/signoz_flamegraphs_hc.png"
     title="Flamegraphs showing exact duration taken by each spans - a concept of distributed tracing"
     width={700}
/>

## Conclusion

OpenTelemetry makes it very convenient to instrument your Spring Boot application. You can then use an open-source APM tool like SigNoz to analyze the performance of your app. As SigNoz offers a full-stack observability tool, you don't have to use multiple tools for your monitoring needs.

You can try out SigNoz by visiting its GitHub repo 👇

<div class="text--center">

[![SigNoz repo](/img/blog/common/signoz_github.png)](https://github.com/signoz/signoz)

</div>

<br></br>
If you are someone who understands more from video, then you can watch the tutorial on how to use OpenTelemetry for Spring Boot application here 👇

<div class="text--center">

<iframe width="560" height="315" src="https://www.youtube.com/embed/YxZb17_LYwQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

</div>

If you want to read more about SigNoz 👇

[Golang Application Performance Monitoring with SigNoz](/blog/monitoring-your-go-application-with-signoz/)

[Nodejs Application Performance Monitoring with SigNoz](/blog/nodejs-opensource-application-monitoring/)