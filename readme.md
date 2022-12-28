# Spring PetClinic Sample Application 
## Running petclinic locally
Petclinic is a [Spring Boot](https://spring.io/guides/gs/spring-boot) application built using [Maven](https://spring.io/guides/gs/maven/) or [Gradle](https://spring.io/guides/gs/gradle/). You can build a jar file and run it from the command line (it should work just as well with Java 11 or newer):


```bash
cd spring-petclinic
./mvnw package
java -jar target/*.jar

# or u can perform 
./mvnw spring-boot:run
```
## Change port if required
* We can use this command to change the port of the spring boot during execution `java -jar spring.jar --server.port=80` or `java -jar -Dserver.port=80 spring.jar`

You can then access petclinic here: http://localhost:8080/

## Update the Maven pom.xml file
* Update the `pom.xml` file as shown here
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
    ...
    <!-- Add Spring Cloud GCP Dependency BOM -->
    <dependencyManagement>
        <dependencies>
          <dependency>
          <groupId>com.google.cloud</groupId>
          <artifactId>spring-cloud-gcp-dependencies</artifactId>
          <version>3.3.0</version>
          <type>pom</type>
          <scope>import</scope>
          </dependency>
      </dependencies>
    </dependencyManagement>
    <dependencies>
      ...
      <!-- Add CloudSQL Starter for MySQL -->
      <dependency>
        <groupId>com.google.cloud</groupId>
        <artifactId>spring-cloud-gcp-starter-sql-mysql</artifactId>
      </dependency>
      ...
    </dependencies>
</project>
```

## Update application.properties file

```bash
# here is the file location
src/main/resources/application-mysql.properties
```

## src/main/resources/application.properties
```bash
# In the last line, add mysql to the spring.profiles.active property
spring.profiles.active=mysql
```
## Run the app with Mysql DB change:
```bash
./mvnw -Dspring.profiles.active=mysql -DskipTests spring-boot:run
```
## Database configuration

In its default configuration, Petclinic uses an in-memory database (H2) which
gets populated at startup with data. The h2 console is automatically exposed at `http://localhost:8080/h2-console`
and it is possible to inspect the content of the database using the `jdbc:h2:mem:testdb` url.
 
A similar setup is provided for MySQL and PostgreSQL in case a persistent database configuration is needed. Note that whenever the database type is changed, the app needs to be run with a different profile: `spring.profiles.active=mysql` for MySQL or `spring.profiles.active=postgres` for PostgreSQL.
