# Object Mapper in Java
The Java DataStax Driver comes with an object mapper that removes boilerplate of writing queries and lets you focus on your application objects. This example shows how to use mapper to build Data Access Objects ( DAOs ) to access Apache Cassandra™ in a Java application.

Contributor(s): [Olivier Michallat](https://github.com/olim7t) - derived from [here](https://github.com/datastax/java-driver/tree/4.x/examples/src/main/java/com/datastax/oss/driver/examples/mapper)

## Objectives

* Demonstrate how to use the Java Driver object mapper to replace the tedious work of DAO recreation in Java. Reference the [documentation](https://docs.datastax.com/en/developer/java-driver/latest/manual/mapper/mapper/) for details about the object mapper.
  
## Project Layout

* [MapperApp.java](/src/main/java/com/datastax/examples/MapperApp.java) - The main application file that uses the [`video`](/src/main/java/com/datastax/examples/mapper/killrvideo/video/) and [`user`](/src/main/java/com/datastax/examples/mapper/killrvideo/user/) DAOs.

## How this Sample Works
The driver provides a simple object mapper which allows us to avoid writing much of the boilerplate code 
required to map query results to and from POJOs.

To use the mapper requires that several different components be annotated in such a way as to allow them to 
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

For additional information and details on how to use the Mapper classes please refer to the documentation available [here](https://docs.datastax.com/en/developer/java-driver/4.3/manual/mapper/).
 
## Setup and Running

### Prerequisites

* Java 8
* A Cassandra cluster is running and accessible through the contacts points and data center identified in [application.conf](/src/main/resources/application.conf)

### Running

To run this application use the following command:

`mvn exec:java -Dexec.mainClass=com.datastax.examples.MapperApp`

This will produce results similar to those below.

```
Reusing existing User[userid=1c8612ce-3ff9-4741-9c29-5f63bbe5d9d4, firstname='test', lastname='user', email='testuser@example.com', createdDate=2019-11-15T17:19:54.129Z]
Logging in with testuser@example.com/password123: Success
Logging in with testuser@example.com/secret123: Failure
Created video [79d302e0-3261-460a-849f-3db992e79899] Join us at DataStax Accelerate 2020
Videos for test user:
  [79d302e0-3261-460a-849f-3db992e79899] Join us at DataStax Accelerate 2020
Latest videos:
  [79d302e0-3261-460a-849f-3db992e79899] Join us at DataStax Accelerate 2020
Videos tagged with apachecassandra:
  [558e036d-a5df-4e1c-9309-e3048d5c34fb] Join us at DataStax Accelerate 2020
Updated name for video 79d302e0-3261-460a-849f-3db992e79899: Join us at DataStax Accelerate 2020, in sunny San Diego!
```

