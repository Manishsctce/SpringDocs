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

