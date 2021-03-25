---
title: Spring Cloud Microservices
categories: [Backend]
tags: java microservices
---

Spring Cloud
I'll create a module in Intellij Idea

---

# spring cloud config server
- Reload All Maven Project (We have to reload all maven project after you create the module).


# add a microservice module called 'authserver'
- add module tag in collaboss's pom.xml
  ```
  <module>authserver</module>
  ```
- h2 console settings (applicaion.yml)
  ```
  spring:
  h2:
    console:
      enabled: true
  datasource:
    url: jdbc:h2:mem:testdb
  ```
  http://localhost:9191/h2-console  
  password : none

# add eureka service

# cloud-gateway service
- application.yml
  ```
  server:
  port: 8989

  spring:
    application:
      name: GATEWAY-SERVICE
    cloud:
      gateway:
        routes:
          - id: auth-service
            uri: lb://AUTH-SERVICE
            predicates:
              - Path=/auth/**
          - id: portal-service
            uri: lb://PORTAL-SERVICE
            predicates:
              - Path=/sbp/**

  eureka:
    client:
      register-with-eureka: true
      fetch-registry: true
      service-url:
        defaultZone: http://localhost:8761/eureka/
    instance:
      hostname: localhost

  ```
- Note: Gateway is not compatible with org.springframework.boot:spring-boot-starter-web  
Related error message: Spring-cloud-gateway application not starting up.