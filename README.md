

# SpringDocs
Spring Notes

## What is the difference between the @ComponentScan and @EnableAutoConfiguration annotations in Spring Boot?

@EnableAutoConfiguration annotation 
- tells Spring Boot to "guess" how you will want to configure Spring, based on the jar dependencies that you have added. 
- For example, If HSQLDB is on your classpath, and you have not manually configured any database connection beans, then Spring will auto-configure an in-memory database.

@ComponentScan 
- tells Spring to look for other components, configurations, and services in the specified package. 
- Spring is able to auto scan, detect and register your beans or components from pre-defined project package. 
- If no package is specified current class package is taken as the root package.
~~~~~~~~~~~~~~~~~~~~~~~

Spring Boot Framework has mainly four major Components.

1. Spring Boot Starters
- combines all related jars into single jar file so that we can add only jar file dependency to our build files. 
- Spring Boot Framework will automatically download all required jars and add to our project classpath

2. Spring Boot AutoConfigurator
- it reduce the Spring Configuration
- almost no or minimal Annotation configuration
- Example: 
@SpringBootApplication = @Configuration + @EnableAutoConfiguration + @ComponentScan

3. Spring Boot CLI
- used to run and test Spring Boot applications from command prompt.

4. Spring Boot Actuator
- Providing Management EndPoints to Spring Boot Applications.
- Spring Boot Applications Metrics.


> Spring Boot Framework internally depends on these two major components: 
1. Groovy 
- it is used to add some defaults like Default import statements
- it has JAR Dependency Resolver to resolve and add all required jar files to Groovy Project classpath.

2. Grape
- it is an Embedded Dependency Resolution engine

==============================
####### MAVEN #########
> It is a software project management and comprehension tool. 
> Based on the concept of a project object model (POM)
- used to build and manage any Java based project

####### POM #######
Note: there should be a single POM file for each project

> All POM files require the project element and three mandatory fields: groupId, artifactId, version.

> Projects notation in repository is groupId:artifactId:version.


packaging	
- defines packaging type such as jar, war etc.

scope	
- defines scope for this maven project. 
- It can be compile, provided, runtime, test and system.

~~~~~~~~~~~~~~~~~~~~~
> Super POM is Maven’s default POM. 
- All POMs inherit from a parent or default (despite explicitly defined or not). 
- This base POM is known as the Super POM, and contains values inherited by default.

> An easy way to look at the default configurations of the super POM is 
- by running the following command: mvn help:effective-pom

## What is Build Lifecycle?
> It is well-defined sequence of phases, which define the order in which the goals are to be executed. 
- here phase represents a stage in life cycle. 



==============================
> To create JAR/WAR/EAR
maven package

> To deploy Web Application
mvn deploy

> To run on Jetty embedded server:
mvn jetty:run

In kafka monitoring what is difference between received bytes and sent bytes and retained bytes?

1. Received Bytes
Definition: The total amount of data (in bytes) that Kafka brokers receive from producers.
Represents:
Incoming data traffic from producer clients.
Includes messages published to topics as well as metadata requests from producers.

2. Sent Bytes
Definition: The total amount of data (in bytes) that Kafka brokers send to consumers.
Represents:
Outgoing data traffic to consumer clients.
Includes messages fetched by consumers, along with metadata and offset-related requests.
Use Case:
Measure the rate of data being consumed from the Kafka cluster.
Helps identify consumer throughput and whether consumers are actively consuming data.

3. Retained Bytes
Definition: The total amount of data (in bytes) stored on Kafka brokers (on disk) for topics and partitions.
Represents:
Persistent data retained on disk due to Kafka’s retention policy.
Includes data that hasn’t been consumed yet or has been retained even after consumption, depending on the retention settings.
Use Case:
Monitor how much disk space is being used by Kafka.
Determine whether disk usage is within capacity or if partitions need to be rebalanced.
Typical Scenario:
High retained bytes means brokers are holding a large amount of data, which could be due to:
A long retention policy.
Consumers falling behind (leading to retained data).
Low consumption rates or inactive consumer groups.


Bytes vs Records
Bytes: Measure the volume of data in terms of size (in bytes).

Includes message payloads, metadata, headers, etc.
Useful for understanding bandwidth and storage consumption.
Records: Measure the volume of data in terms of the number of messages (or records).

Focuses on the count of Kafka messages, irrespective of their size.
Useful for understanding the message throughput.


Received Records: The total number of messages (records) received by Kafka brokers from producer clients.

Sent Records : The total number of messages (records) sent by Kafka brokers to consumer clients.
