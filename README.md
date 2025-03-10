

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


{
  "notificationId": "string", 
  "timestamp": "ISO 8601 timestamp",
  "sourceApplication": "string",
  "eventType": "string",
  "severity": "string",
  "data": {
    "subject": "string",
    "body": "string",
    "details": {
      "key1": "value1",
      "key2": "value2"
    }
  },
  "metadata": {
    "correlationId": "string",
    "partitionKey": "string",
    "additionalInfo": {
      "key": "value"
    }
  }
}


Top-Level Fields

notificationId (string): A unique identifier for the notification. Can be a UUID.
timestamp (ISO 8601 timestamp): The time the notification was generated. Use formats like "2024-12-05T12:34:56Z".
sourceApplication (string): The application or microservice that generated the notification. Example: "OrderService".
eventType (string): A classification of the event that triggered the notification. Example: "OrderCreated", "UserRegistered".
severity (string): Indicates the urgency or priority of the notification. Values can include:
"INFO"
"WARN"
"ERROR"
"CRITICAL"
data (object):

subject (string): A brief description of the notification. Example: "New Order Created".
body (string): Detailed information about the notification. Example: "An order with ID 12345 has been created."
details (object): A key-value map to store additional information specific to the event. Example:
json
Copy code
{
  "orderId": "12345",
  "userId": "67890"
}
metadata (object):

correlationId (string): A unique identifier to correlate this notification with related events or transactions.
partitionKey (string): A key used for Kafka partitioning. Helps group related messages together. Example: "orderId".
additionalInfo (object): A flexible map for including optional or auxiliary metadata.
---------------------------------
#!/bin/bash

# Directory or files to process
INPUT_FILES="path/to/files/*"  # Replace with your actual file path or directory

# REST API endpoint
API_URL="https://example.com/api/endpoint"  # Replace with your API endpoint

# Initialize total to 0
total=0

# Process each file
for file in $INPUT_FILES; do
  if [[ -f "$file" ]]; then
    # Extract numbers from lines containing the phrase
    number=$(grep "The total request count is" "$file" | sed -n 's/.*The total request count is \([0-9]*\).*/\1/p')

    # Add the extracted number to the total (if found)
    if [[ ! -z "$number" ]]; then
      total=$((total + number))
    fi
  fi
done

# Get the current date in ISO 8601 format
current_date=$(date -u +"%Y-%m-%dT%H:%M:%SZ")

# Prepare the JSON payload
json_payload=$(cat <<EOF
{
  "date": "$current_date",
  "total_request_count": $total
}
EOF
)

# Send the JSON payload in a POST request to the API
response=$(curl -s -X POST -H "Content-Type: application/json" -d "$json_payload" "$API_URL")

# Print the response from the API
echo "Response from API: $response"

-------------------------
file_pattern="consumer_usage_"
valid_numbers=("121" "221" "321" "421")
api_url="https://your-api-endpoint.com"
current_date=$(date +"%Y-%m-%d")

# Initialize a counter for the total extracted numbers
total_count=0

# Find files matching the pattern and process them
find . -name "${file_pattern}*" -mtime +20 -type f | while read -r file; do
    # Extract the number part from the filename
    base_name=$(basename "$file")
    for number in "${valid_numbers[@]}"; do
        if [[ $base_name == "${file_pattern}${number}"* ]]; then
            # If the filename matches, search for the line in the file
            extracted_number=$(grep -oP "The total request count is \d+ node : \K\d+" "$file")
            if [[ -n $extracted_number ]]; then
                total_count=$((total_count + extracted_number))
            fi
        fi
    done
done
------------------------------------------
/**
     * Recursively process YAML data of any structure.
     *
     * @param data       YAML data (can be Map, List, or primitive type).
     * @param currentKey The current key being processed.
     * @param currentPath The hierarchical path of the current key (for storing in maps).
     */
    private static void processYaml(Object data, String currentKey, String currentPath) {
        if (data instanceof Map) {
            // If the data is a Map, iterate over each entry
            Map<String, Object> map = (Map<String, Object>) data;
            for (Map.Entry<String, Object> entry : map.entrySet()) {
                String key = entry.getKey();
                Object value = entry.getValue();
                String newPath = currentPath.isEmpty() ? key : currentPath + "." + key;

                // Check for vault.config.* or runtime.vault.path.*
                if (newPath.startsWith("vault.config.")) {
                    addToNestedMap(vaultConfigNestedMap, "vault.config.", newPath, value);
                } else if (newPath.startsWith("runtime.vault.path.")) {
                    addToNestedMap(runtimeVaultPathNestedMap, "runtime.vault.path.", newPath, value);
                }

                // Recursively process further
                processYaml(value, key, newPath);
            }
        } else if (data instanceof List) {
            // If the data is a List, process each item in the list
            List<Object> list = (List<Object>) data;
            for (int i = 0; i < list.size(); i++) {
                String listPath = currentPath + "[" + i + "]";
                processYaml(list.get(i), currentKey, listPath);
            }
        }
    }

    /**
     * Adds a nested property to the map of maps based on the prefix.
     *
     * @param targetMap The target map to store the nested property.
     * @param prefix    The prefix to strip from the path (e.g., "vault.config.").
     * @param fullPath  The full hierarchical path of the property.
     * @param value     The value of the property.
     */
    private static void addToNestedMap(Map<String, Map<String, Object>> targetMap, String prefix, String fullPath, Object value) {
        // Remove the prefix (e.g., "vault.config.") to extract the remaining path
        String remainingPath = fullPath.substring(prefix.length());

        // Extract the first part (e.g., "dev") and the sub-key (e.g., "javax")
        int dotIndex = remainingPath.indexOf(".");
        if (dotIndex == -1) return; // If no further structure, skip

        String topKey = remainingPath.substring(0, dotIndex); // e.g., "dev"
        String subKey = remainingPath.substring(dotIndex + 1); // e.g., "javax"

        // Get or create the nested map for the top-level key
        Map<String, Object> nestedMap = targetMap.computeIfAbsent(topKey, k -> new HashMap<>());

        // Add the sub-key and value to the nested map
        nestedMap.put(subKey, value);
    }

---------------------------------





