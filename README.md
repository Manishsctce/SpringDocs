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
