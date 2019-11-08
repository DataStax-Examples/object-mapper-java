# Inserting and retrieving Blobs in Java
This demonstrates how to use mapper to provide DAO's to access Cassandra

Contributors: [Olivier Michallat](https://github.com/olim7t), derived from [here](https://github.com/datastax/java-driver/tree/4.x/examples/src/main/java/com/datastax/oss/driver/examples/mapper)

## Objectives

* To demonstrate how to use mapper to replace the tedious work DAO recreation in Java. Please refer [here](https://docs.datastax.com/en/developer/java-driver/4.3/manual/mapper/mapper/) for more details on using object mapper.
  
## Project Layout

* MapperApp.java - The main application file 

## How this Sample Works
The mapper interface is the top-level entry point to mapping features. It wraps a core driver session, and acts as a factory of DAO objects that will be used to execute requests. This app creates a top level
mapper in the default keyspace killrvideo. This mapper interface acts as a factory to create and maintain the 
* userDAO
* videoDAO

These two DAO's are used to interact with the Cassandra cluster. 
 
## Setup and Running

### Prerequisites

* Java 8
* An Apache Cassandra(R) cluster is running and accessible through the contacts points and data center identified in [application.conf](/src/main/resources/application.conf)

### Running

e.g.
To run this application use the following command:

`mvn exec:exec`

This will create a new keyspace killrvideo and many tables in the keyspace:

`
Insert rows into the users, videos and the other tables
`

