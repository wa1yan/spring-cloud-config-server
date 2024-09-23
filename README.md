# Spring Cloud Config Server
####

## Background
this is background test

## Pros and Cons
this is pros and cons test

## Guide

Dependency

Note: cloud-config-monitor dependency need to add on config server because we will use git-hub webhook to trigger change event on config server so configuration data will call monitor endpoint.
```
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-config-server</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-bus-kafka</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        <dependency> 
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-config-monitor</artifactId>
        </dependency>
```

Configuration
```
server:
  port: 8888
spring:
  application:
    name: config-server
  cloud:
    config:
      server:
        git:
          uri: https://github.com/wa1yan/spring-cloud-config-data
          force-pull: true
          skip-ssl-validation: true
          timeout: 10
          username: [username]
          password: [password]
          default-label: main
    bus:
      enabled: true
    stream:
      kafka:
        binder:
          brokers: http://localhost:29092
#  kafka:
#    bootstrap-servers:
#      - http://localhost:29092

management:
  endpoints:
    web:
      exposure:
        include: '*'
```

Configuraiton server bus refresh endpoint
```
# curl -X POST http://[config-server-url]/actuator/bus-refresh
```
