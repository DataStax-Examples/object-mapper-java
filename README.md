# Object Mapper in Java
The [Java DataStax Driver](https://docs.datastax.com/en/developer/java-driver/latest/) comes with an object mapper that removes boilerplate of writing queries 
and lets you focus on your application objects. This example shows how to use mapper to build Data Access Objects ( DAOs ) to access Apache Cassandra™ in a Java 
application.

Contributor(s): [Olivier Michallat](https://github.com/olim7t) - derived from 
[here](https://github.com/datastax/java-driver/tree/4.x/examples/src/main/java/com/datastax/oss/driver/examples/mapper)

## Objectives

* Demonstrate how to use the Java Driver object mapper to replace the tedious work of DAO recreation in Java. Reference the 
[documentation](https://docs.datastax.com/en/developer/java-driver/latest/manual/mapper/mapper/) for details about the object mapper.
  
## Project Layout

* [MapperApp.java](/src/main/java/com/datastax/examples/MapperApp.java) - The main application file that uses the 
[`video`](/src/main/java/com/datastax/examples/mapper/killrvideo/video/) and [`user`](/src/main/java/com/datastax/examples/mapper/killrvideo/user/) DAOs.

## How this Sample Works
The driver provides a simple object mapper which allows us to avoid writing much of the boilerplate code 
required to map query results to and from POJOs.

To use the mapper requires that several components be annotated in such a way as to allow them to 
work together:

* Mapper - This is the entry point for this mapper which wraps the core driver session and acts as a factory for 
creating the DAO objects.  In this example the mapper is [KillrVideoMapper](/src/main/java/com/datastax/examples/mapper/killrvideo/KillrVideoMapper.java).
* DAO - Acts as the interface which defines the set of operations which can be performed on an entity.  In this example 
[VideoDao](/src/main/java/com/datastax/examples/mapper/killrvideo/video/VideoDao.java) and 
[UserDao](/src/main/java/com/datastax/examples/mapper/killrvideo/user/UserDao.java) are DAO classes.
* Entity - This is a class which will be mapped to a Cassandra table or UDT.  In this example 
[Video](/src/main/java/com/datastax/examples/mapper/killrvideo/video/Video.java),  
[VideoByTag](/src/main/java/com/datastax/examples/mapper/killrvideo/video/VideoByTag.java),  and
[User](/src/main/java/com/datastax/examples/mapper/killrvideo/user/User.java) are Entity classes
* Query Provider - These provide a method to define queries which cannont be expressed as static strings.  
In this example 
[CreateVideoQueryProvider](/src/main/java/com/datastax/examples/mapper/killrvideo/video/CreateVideoQueryProvider.java),  
[LoginQueryProvider](/src/main/java/com/datastax/examples/mapper/killrvideo/user/LoginQueryProvider.java) and 
[CreateUserQueryProvider](/src/main/java/com/datastax/examples/mapper/killrvideo/user/CreateUserQueryProvider.java) are Query Provider classes.

For additional information and details on how to use the Mapper classes please refer to the documentation available 
[here](https://docs.datastax.com/en/developer/java-driver/4.3/manual/mapper/).
 
## Setup and Running

### Prerequisites

* JDK 14
* A Cassandra cluster is running and accessible through the contacts points and data center identified in [application.conf](/src/main/resources/application.conf)
#### Building
At the project root level

```mvn clean package```

This builds the JAR file located at `target/object-mapper-1.0.jar`

#### Run the program
To run this application, use the following command:

```java -jar target/object-mapper-1.0.jar```

This will produce results similar to those below.

```
Created User[userid=ce662229-e371-4469-843a-b3e16d9fb8fa, firstname='test', lastname='user', email='testuser@example.com', createdDate=2020-04-16T20:37:17.596601Z]
Logging in with testuser@example.com/password123: Success
Logging in with testuser@example.com/secret123: Failure
Created video [d40e409e-4949-4728-89dc-a4374ee78b17] Accelerate: A NoSQL Original Series (TRAILER)
Videos for test user:
  [d40e409e-4949-4728-89dc-a4374ee78b17] Accelerate: A NoSQL Original Series (TRAILER)
Latest videos:
  [d40e409e-4949-4728-89dc-a4374ee78b17] Accelerate: A NoSQL Original Series (TRAILER)
Videos tagged with apachecassandra:
  [d40e409e-4949-4728-89dc-a4374ee78b17] Accelerate: A NoSQL Original Series (TRAILER)
Updated name for video d40e409e-4949-4728-89dc-a4374ee78b17: Accelerate: A NoSQL Original Series - join us online!
```

