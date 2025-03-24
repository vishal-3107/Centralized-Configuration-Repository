## This repository serves as the centralized configuration source for microservices using Spring Cloud Config Server. 
## It contains environment-specific configuration files that the Config Server will read and serve to client applications.

## 📌 Structure
    config-repo/
    ├── limits-service.properties      # Default configuration (applies to all environments)
    ├── limits-service-dev.properties  # Development environment configuration
    ├── limits-service-qa.properties   # QA environment configuration

## 🚀 Usage

## 1️⃣ Spring Cloud Config Server Setup

## To connect this repository with the Spring Cloud Config Server, update your application.yml in the Config Server project:
    server:
    port: 8888

    spring:
        cloud:
            config:
                server:
                    git:
                        uri: https://github.com/your-username/central-config-repo
                        clone-on-start: true

## 2️⃣ Fetching Configurations

    Once the Config Server is running, microservices can fetch their configurations dynamically.
    ->  Fetch Default Configuration:
        http://localhost:8888/limits-service/default
    ->  Fetch Dev Environment Configuration:
        http://localhost:8888/limits-service/dev
    ->  Fetch QA Environment Configuration:
        http://localhost:8888/limits-service/qa

## 3️⃣ Spring Boot Client Configuration

    Each microservice should include the following in its bootstrap.yml:
    spring:
        application:
            name: limits-service
        cloud:
            config:
                uri: http://localhost:8888
                profile: dev  # Change this to 'qa' or other environments as needed
