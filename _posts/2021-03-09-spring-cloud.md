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
