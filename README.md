# Template for Microservices with Spring Cloud

## Introducing
![Microservices-template](/assets/microservices.png)

This project is a lightweight and preconfigured starter template that sets up the foundational infrastructure for building microservices using Spring Cloud. It includes essential components to enable service discovery, routing, and centralized configuration management.

## 🔧 Included Components:
✅ **Spring Boot 3.4.6** – The project inherits Spring Boot 3.4.6 to all modules.

✅ **Spring Cloud BOM** – The project inherits Spring Boot and imports Spring Cloud dependencies via a managed BOM.

✅ **Spring Cloud Config Server** – Centralized externalized configuration for all services

✅ **Eureka Server** – Service registry for discovering and managing microservices dynamically

✅ **Spring Cloud Gateway** – API gateway for intelligent routing and load balancing

> [!IMPORTANT]
> Doesn't include Structured Modular Design and Sample Services with their Feign Clients

> [!WARNING]
> Actually Spring Boot has a newer version 3.5.0 but it's not compatible with Spring Cloud latest version 2024.0.1, at the time Spring Boot 3.5.0 is compatible with 2025.0.0-RC1, you can change it by adding to the pom this lines below   

``PARENT POM.XML``
```xml

<!-- repositories needs to be added to the pom.xml -->
<repositories>
    <repository>
        <id>spring-milestones</id>
        <name>Spring Milestones</name>
        <url>https://repo.spring.io/milestone</url>
        <snapshots>
            <enabled>false</enabled>
        </snapshots>
    </repository>
</repositories>

<!-- All this lines already exists, you only need to update the version -->
<dependencyManagement>
<dependencies>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-dependencies</artifactId>
        <version>2025.0.0-RC1</version> <!-- change this to 2025 version -->
        <type>pom</type>
        <scope>import</scope>
    </dependency>
</dependencies>
</dependencyManagement>

<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>3.5.0</version> <!-- change this to the lastest Spring Boot version as needed -->
    <relativePath/>
</parent>
```




## Configurations
It brings all configurations in config server like it shows in the diagram [Microservices-template](#Introducing) this are the steps you should follow after creating new modules

1. When you add your first microservice you should add the next dependencies ``netflix-eureka-client`` `config-client`
2. The application.yml needs to be using ``optional:configserver:http://localhost:8888`` in ``spring.config.import`` to the route of config-server and de application name should be the same as the config folder in this example we'll call the ``spring.application.name=module-service``
3. Example: ``module-service.yml`` should be located in ``[config-server].../resources/config`` with all configurations like a monolithic ``application.yml`` server port, database url, user, password, and all you need all in that ``module-service.yml`` located in ``config-server``
4. And that's it, now you should start servers in this order: 
 > ``[config-server]`` -> ``[eureka-server]`` -> ``[gateway-service]`` -> ``[all-others-msvc]``
## Purpose of this template

This template is ideal for bootstrapping new microservices projects by providing a working skeleton of the core infrastructure. Developers can plug in their business services later, allowing for rapid and scalable development aligned with modern cloud-native practices.
