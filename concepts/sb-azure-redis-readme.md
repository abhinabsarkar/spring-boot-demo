# Spring Boot App running locally & invoking Azure Redis Cache

![alt txt](/images/sb-azure-redis.jpg)

## Running this app
Pre-requisites
* Java 8
* Maven
* Azure subscription running Azure Cache for Redis

Create an Azure Cache for Redis. 

```bash
az redis create --location canadacentral --name redis-cache --resource-group rg-demo --sku Basic --vm-size c0
```

Update the following in the application.properties within the source code. The values are available in the Azure Cache for Redis. 
* spring.redis.host
* spring.redis.password
* spring.redis.port

```bash
# Go to the code folder
cd code
# Build the JAR file using Maven
mvn clean package
# Run the application 
mvn spring-boot:run
```

Browse by visiting `http://localhost:8080/`

![alt txt](/images/sb-redis-sample.jpg)

You can monitor the cache in Azure by going to the Redis Cache resource --> Overview --> Console. Type `monitor` in the console. The monitoring console will start showing logs once messages are stored in the cache.