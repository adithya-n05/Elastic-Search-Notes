
## Course Overview

In this course, you will learn how to write complex queries against data stored in Elasticsearch. These queries allow you to define conditions for matching data and are applicable to various use cases.

### Use Cases

The skills you acquire in this course can be applied to a wide range of use cases, such as:

- Implementing search functionality on websites or within applications
- Data analysis
- Application Performance Monitoring (APM)
- Log management
- Server monitoring
- Security

The course does not focus on a specific use case, allowing you to adapt the concepts to your specific needs.

### Building a Modern Search Engine

The course will provide you with the knowledge required to build a modern search engine. This includes understanding and implementing the following concepts:

- Handling synonyms: Managing different terms that have the same or similar meanings.
- Stemming: Reducing words to their base or root form to improve search accuracy.
- Search-as-you-type: Providing real-time suggestions as users type in their search queries.
- Auto-completion: Offering relevant suggestions for completing user queries.
- Tuning relevance scores: Adjusting the ranking of search results to improve relevance.

### Aggregations for Data Analysis

In addition to query writing, the course will cover aggregations, a fundamental feature for analyzing large sets of data. Aggregations allow you to perform calculations, summaries, and statistical analyses on your data.

### Summary

This course will equip you with the skills to write complex queries in Elasticsearch, applicable to various use cases. You will learn concepts essential for building a modern search engine and understand how to leverage aggregations for data analysis.

## Further overview

In this course, you will learn how to write complex queries in Elasticsearch, a powerful open-source analytics and full-text search engine. Elasticsearch is commonly used to enable search functionality for various applications, such as blogs, webshops, and more.

### Building Powerful Search Functionality

With Elasticsearch, you can build sophisticated search functionality similar to popular search engines like Google. This includes features such as:

- Auto-completion: Offering suggestions as users type their search queries.
- Correcting typos: Handling and providing suggestions for misspelled words.
- Highlighting matches: Making it easy for users to identify relevant search results.
- Handling synonyms: Managing different terms with similar meanings.
- Adjusting relevance: Fine-tuning the ranking of search results based on factors like ratings.

Additionally, Elasticsearch allows for filtering and sorting search results based on various criteria, such as price, brand, size, color, and more. The course covers these advanced search capabilities.

### Analyzing Structured and Unstructured Data

Elasticsearch is not limited to full-text search. It also supports querying and aggregating structured data, making it a versatile analytics platform. You can perform calculations, summaries, and statistical analyses on your data and visualize the results in charts and graphs.

Examples of analytics use cases include:

- Application Performance Management (APM): Analyzing logs and system metrics to monitor application performance.
- Sales forecasting: Using machine learning to predict sales based on historical data.
- Anomaly detection: Identifying unusual patterns or deviations from normal behavior.

While the course primarily focuses on search functionality, it provides an overview of other Elasticsearch capabilities, giving you a solid foundation to explore additional features.

### Elasticsearch Basics

Elasticsearch stores data as documents, which are JSON objects representing units of information. Documents consist of fields, similar to columns in a relational database. To query documents, you use a REST API and send JSON-based queries to Elasticsearch.

Elasticsearch is written in Java and built on Apache Lucene. It is known for its scalability, allowing for efficient search and analysis of large volumes of data. Many large companies rely on Elasticsearch for their search and analytics needs, and a thriving community provides support and resources.

In the next section, we will explore the Elastic Stack, an ecosystem of tools and technologies that complement Elasticsearch.

## The Elastic Stack

This course primarily focuses on Elasticsearch, but it's important to briefly discuss the other technologies that form the Elastic Stack.

### Kibana

Kibana is an analytics and visualization platform that works in conjunction with Elasticsearch. It provides a web interface to easily visualize data from Elasticsearch and create various types of visualizations, such as pie charts and line charts. Kibana allows you to monitor performance, configure change detection, and perform forecasting. It acts as an interface to Elasticsearch, utilizing the same REST API to query and display results. With Kibana, you can create dashboards for different user roles, such as system administrators, developers, and management.

### Logstash

Logstash is a data processing pipeline tool that is commonly used to process logs from applications and send them to Elasticsearch. However, Logstash has evolved into a more general-purpose tool for data processing. It receives data as events, which can be logs, orders, messages, etc. Logstash pipelines consist of three stages: inputs, filters, and outputs. Inputs receive events, filters process and transform the data, and outputs send the processed data to various destinations, such as Elasticsearch or external systems. Logstash supports plugins for inputs, filters, and outputs, providing flexibility in data processing.

### X-Pack

X-Pack is a pack of additional features that enhance Elasticsearch and Kibana. It includes:

- Security: Provides authentication and authorization for Elasticsearch and Kibana, allowing integration with LDAP, Active Directory, and other technologies. Users and roles can be managed with granular access control.
- Monitoring: Enables monitoring and alerting for the Elastic Stack, providing insights into CPU and memory usage, disk space, and other important metrics. Alerting can be set up to notify when specific conditions are met.
- Reporting: Allows exporting Kibana visualizations and dashboards as PDF reports, which can be generated on-demand or scheduled. Reports can be customized with logos and shared with stakeholders.
- Machine Learning: Provides machine learning capabilities in Elasticsearch and Kibana, including anomaly detection and forecasting. Machine learning jobs can monitor data and trigger alerts based on abnormal behavior.
- Graph: Analyzes relationships in data to discover connections and relevance. It can be used to suggest related products, recommend content, or explore connections in data. Graph provides a plugin for Kibana to visualize data as an interactive graph.
- SQL: Enables querying Elasticsearch with SQL syntax, allowing developers familiar with relational databases to write SQL queries. Elasticsearch translates SQL queries into the Query DSL format.

### Beats

Beats are lightweight data shippers that collect and send data to Logstash or Elasticsearch. Filebeat is commonly used to collect log files, while Metricbeat collects system-level and service metrics. Beats are installed on servers and can be configured to collect various types of data, such as logs, metrics, or network data. They provide a lightweight and efficient way to ingest data into the Elastic Stack.

### The Elastic Stack Architecture

In the Elastic Stack architecture, Elasticsearch serves as the central data store. Data can be ingested into Elasticsearch using Beats, Logstash, or directly through the Elasticsearch API. Kibana sits on top of Elasticsearch and provides a user interface to visualize and analyze the data retrieved from Elasticsearch. X-Pack enhances Elasticsearch and Kibana with additional features like security, monitoring, reporting, machine learning, graph analysis, and SQL querying.

The Elastic Stack, formerly known as the ELK stack, refers to Elasticsearch, Logstash, and Kibana. However, with the introduction of Beats and X-Pack, the Elastic Stack now encompasses a broader range of technologies and capabilities. The Elastic Stack is highly customizable, scalable, and widely used for various use cases.

Please note that this course focuses primarily on Elasticsearch and its search capabilities, providing a foundation for further exploration and utilization of the Elastic Stack's additional features.

## Common Elasticsearch Architectures

Let's explore a couple of common architectures that demonstrate how Elasticsearch is commonly used in different scenarios.

### Basic Search Integration

Suppose we have an e-commerce application running on a web server, with data stored in a database. Initially, the search functionality relies on the database, but we decide to improve it using Elasticsearch. To integrate Elasticsearch into the existing architecture, the web application sends search queries to Elasticsearch via HTTP requests or using client libraries. Elasticsearch processes the queries and returns results to the application, which then sends them back to the user's browser. Whenever a new product is added or updated in the database, it should also be added or updated in Elasticsearch to ensure the search index stays up to date.

**Example Code (Python):**

```python
import requests

# Send a search query to Elasticsearch
def search(query):
    url = "http://localhost:9200/products/_search"
    payload = {
        "query": {
            "match": {
                "title": query
            }
        }
    }
    response = requests.get(url, json=payload)
    data = response.json()
    # Process and return the search results
    return data["hits"]["hits"]

# Usage example
results = search("shoes")
```

### Adding Kibana for Monitoring and Visualization

As the e-commerce business grows, there is a need for a dashboard to monitor the number of orders, revenue, and other metrics. To save time, Kibana is chosen as the visualization tool. Kibana, being a web interface for Elasticsearch, doesn't require data to be added separately. It only needs to be configured to connect to Elasticsearch. By running Kibana on a dedicated machine or virtual machine, it can retrieve data from Elasticsearch and provide a customizable dashboard for business insights.

### Monitoring with Metricbeat

As website traffic increases, there is a need to monitor system-level metrics to ensure performance and scalability. Metricbeat, a lightweight data shipper, is used to collect metrics such as CPU usage and memory usage. Metricbeat sends data directly to Elasticsearch using an Elasticsearch ingest node, a feature that allows for simple data transformation. With system metrics stored in Elasticsearch, Kibana can visualize and analyze the data. Metricbeat can also configure a default dashboard within Kibana, making it easy to monitor system performance.

### Analyzing Logs with Filebeat

To gain insights from access and error logs of the web server, Filebeat is employed. Filebeat collects log files and sends them to Elasticsearch for storage and analysis. By starting Filebeat, the logs are automatically processed and stored in Elasticsearch. Filebeat includes built-in modules for common log formats, making configuration effortless. The logs can be visualized and analyzed in Kibana, providing valuable information such as response times, error rates, and more.

### Event Processing with Logstash

As the e-commerce application and development team expand, more data needs to be processed and analyzed. Event data, such as product additions to the cart, requires advanced processing and enrichment. Logstash is introduced to centralize event processing and provide flexibility. Web servers send events to Logstash over HTTP, where they are processed according to custom instructions. Processed events are then sent to Elasticsearch for storage and analysis. Metricbeat and Filebeat can also send data to Logstash for custom processing if necessary. This architecture reduces complexity and ensures event processing is consolidated in one place.

### Long-Term Architecture with Logstash

In the long term, the ideal approach is to migrate all event processing to Logstash pipelines. This would involve sending event data exclusively to Logstash, whether it is from web servers, Metricbeat, or Filebeat. By centralizing event processing, the web application remains focused on querying Elasticsearch rather than modifying data directly. In this ideal scenario, read-only access to Elasticsearch is sufficient for the web application. However, in reality, modifications may still occur depending on specific use cases.

These examples demonstrate typical architectures that evolve over time as Elasticsearch and the Elastic Stack are integrated into existing systems. While variations and other use cases exist, these examples highlight the core functionalities and benefits of Elasticsearch in real-world applications.

## Elasticsearch Architecture

After successfully installing Elasticsearch and Kibana, let's delve into the architecture of Elasticsearch.

### Nodes and Clusters

When Elasticsearch starts up, it starts a node, which is an instance of Elasticsearch responsible for storing data. Multiple nodes can be run to store large amounts of data. Each node holds a portion of the data. This enables data storage across multiple machines or virtual machines, allowing for storing terabytes of data even if each machine has limited disk capacity. It's important to note that a node refers to an instance of Elasticsearch, not necessarily a physical machine. In development environments, multiple nodes can be started on the same machine. However, in production environments, it is recommended to separate nodes onto dedicated machines, virtual machines, or containers.

Nodes belong to a cluster, which is a collection of related nodes that collectively hold all the data. Although multiple clusters can exist, typically one cluster is sufficient. Clusters are independent of each other by default, although cross-cluster searches are possible. Separating clusters can be beneficial when different clusters serve different purposes, such as search and application performance management. However, for most use cases, a single cluster is sufficient.

### Forming a Cluster

Starting an Elasticsearch node automatically forms a cluster. When a node starts, it either joins an existing cluster if configured to do so or creates its own cluster with only that node. Even if there is only a single node, it is still considered part of a cluster. Having a single node poses availability and scalability concerns, but for development purposes, a single-node cluster is acceptable.

### Documents, Indices, and Data Organization

Data in Elasticsearch is organized into documents, which are JSON objects containing desired data. When a document is indexed, the original JSON object is stored alongside metadata used by Elasticsearch internally. For example, a document representing a person could contain fields like "name" and "country." Elasticsearch stores the JSON object within the "_source" field and adds metadata.

Documents are grouped logically within indices. An index is a collection of documents with similar characteristics and logical relationships. For instance, a document representing a person could be stored in an index named "people," while another index named "departments" could store department documents. An index can contain any number of documents without a hard limit. During search queries, the index is specified to retrieve documents.

**Key Takeaways:**
- An Elasticsearch cluster consists of nodes that store data.
- Nodes are instances of Elasticsearch and can run on physical or virtual machines, or within containers.
- Data is stored as documents, which are JSON objects representing various entities.
- Documents are organized into indices, which group related documents.
- A cluster is formed automatically when a node starts, and a single node is sufficient for development purposes.

## Exploring Elasticsearch Cluster

Now that we have Elasticsearch up and running, let's explore the cluster using the Console tool in Kibana.

1. Open the Console tool in Kibana by expanding the menu and clicking "Dev Tools," located within the "Management" group.

2. The Console tool allows us to communicate with the Elasticsearch cluster. Think of it as a way to interact with Elasticsearch using commands.

3. In the Console tool, we can run different types of commands to perform actions on the cluster. These commands resemble the instructions we give to Elasticsearch.

4. To retrieve information about the cluster's health, we use the following command:

   ```HTTP
   GET /_cluster/health
   ```

   This command asks Elasticsearch to provide us with the health information of the cluster.

5. Let's run the command and see the result. The response will be displayed on the right-hand side of the Console tool. It will show a JSON object containing information about the cluster, such as its name and status.

   ```json
   {
     "cluster_name": "elasticsearch",
     "status": "green",
     ...
   }
   ```

   Here, "elasticsearch" is the default name of the cluster, and "green" indicates that the cluster is healthy.

6. Now, let's explore the nodes in the cluster. We can use the following command:

   ```HTTP
   GET /_cat/nodes?v
   ```

   This command asks Elasticsearch to provide information about the nodes in the cluster.

7. Running this command will display a table with basic details about the nodes, such as their IP addresses, names, and performance measures.

   ```plaintext
   ip           heap.percent ram.percent cpu load_1m load_5m load_15m node.role  master name
   127.0.0.1           8          87  11    1.23    0.87     0.45 mdi        -      node-1
   ```

   In this example, we have one node with the name "node-1".

8. We can also check the indices within the cluster using the following command:

   ```HTTP
   GET /_cat/indices?v
   ```

   This command asks Elasticsearch to provide information about the indices in the cluster.

9. Running this command will display a table with the indices. Since we haven't added any indices yet, the result will be empty.

   ```plaintext
   health status index        uuid                   pri rep docs.count docs.deleted store.size pri.store.size
   ```

10. However, Elasticsearch has some system indices that store various things, including Kibana's configuration. These system indices are usually hidden by default.

11. To view the system indices, add the query parameter "expand_wildcards" to the command:

    ```HTTP
    GET /_cat/indices?v&expand_wildcards=all
    ```

12. Running this command will show the system indices along with their details.

This concludes our exploration of the Elasticsearch cluster using the Console tool. In the following lectures, we will dive deeper into the cluster's internals.

Remember, the commands we used (GET /_cluster/health, GET /_cat/nodes, GET /_cat/indices) are specific instructions that you can run in the Console tool to interact with Elasticsearch. The response you receive will depend on the current state and configuration of your Elasticsearch cluster.

## Running Queries with cURL

In addition to using Kibana's Console tool, you can also run queries using cURL, a command-line tool for making HTTP requests. This section will guide you through running queries with cURL.

1. Ensure that cURL is installed on your system. Most systems come with cURL pre-installed. If you need to install it, you can find a download link attached to this lecture.

2. Open a terminal or command prompt to run cURL commands.

3. To start, let's run the simplest cURL command by specifying the endpoint of our Elasticsearch cluster. If you are using Elastic Cloud, use the Elasticsearch endpoint, not the Kibana endpoint.

   ```shell
   curl http://localhost:9200
   ```

   This command sends a GET request to the specified endpoint and retrieves information from Elasticsearch.

4. When running the command, you may encounter a certificate error if you are using a local setup. This error occurs because Elasticsearch generates a self-signed certificate that is not trusted by cURL.

   - To bypass the certificate error, you can use the `--insecure` flag:

     ```shell
     curl --insecure https://localhost:9200
     ```

     This flag tells cURL to ignore the certificate error. However, keep in mind that this is not recommended for production environments.

   - A more secure approach is to provide cURL with the CA certificate using the `--cacert` argument:

     ```shell
     curl --cacert config/certs/ca.crt https://localhost:9200
     ```

     Here, we specify the path to the CA certificate. Adjust the path based on your Elasticsearch configuration.

5. If authentication is required to access your Elasticsearch cluster, you can use the `-u` argument to provide the username:

   ```shell
   curl -u username --cacert config/certs/ca.crt http://localhost:9200
   ```

   When running the command, cURL will prompt you to enter the password associated with the provided username.

   - As an alternative, you can supply the password along with the username:

     ```shell
     curl -u username:password --cacert config/certs/ca.crt https://localhost:9200
     ```

     This approach avoids the password prompt but exposes the password within your terminal, so use it with caution.

6. To send data along with the request, such as when searching for data, you need to specify the `-d` argument followed by a JSON object representing the query.

   - Note: The example query below assumes an existing index named "products," but we will create it later in the course.

     ```shell
     curl -u elastic --cacert config/certs/http_ca.crt -X POST -H "Content-Type: application/json" -d '{
       "query": {
         "match_all": {}
       }
     }' https://localhost:9200/products/_search
     ```

     In this example, we send a POST request to the `/products/_search` endpoint with a JSON object representing the query.

     - The `-X POST` argument specifies the HTTP verb as POST.
     - The `-H` argument sets the Content-Type header to `application/json`.
     - The `-d` argument specifies the JSON data to be sent.

7. If you encounter any issues, ensure that the arguments are in the correct order and properly formatted. cURL can be sensitive to the order of arguments.

Remember, cURL is just one option for making HTTP requests to Elasticsearch. You can also use other HTTP clients, such as Postman, to achieve the same results.

## Replication in Elasticsearch

In addition to sharding, replication plays a crucial role in Elasticsearch for ensuring fault tolerance and availability of data. Let's explore replication and its significance in Elasticsearch.

### Introduction to Replication

When a shard is stored on a node, there is a risk of data loss if that node experiences a failure, such as a disk failure. To mitigate this risk, replication is used. Replication creates copies of each shard, known as replica shards, to provide fault tolerance and failover mechanisms.

Elasticsearch supports replication natively, and it is enabled by default with zero configuration. This is a significant advantage compared to many other databases where replication setup can be complex and time-consuming.

### How Replication Works

Replication in Elasticsearch is configured at the index level and operates alongside sharding.

- Each index consists of one or more shards, which can be distributed across multiple nodes.
- Replication creates copies of each shard called replica shards.
- A shard replicated one or more times is referred to as a primary shard.
- The primary shard and its replica shards form a replication group.

Replica shards are fully functional copies of the primary shard and can serve search requests just like the primary shard.

### Advantages of Replication

1. **Data Redundancy**: Replica shards provide redundancy and ensure that data is not lost even if the node storing the primary shard fails. Replica shards are stored on different nodes than their primary shard counterparts, ensuring data availability.

2. **Fault Tolerance**: If a node fails, there will still be at least one copy of a shard's data available on a different node. The number of available copies depends on the number of replicas configured for the index and the number of nodes in the cluster.

3. **Increased Availability**: Replication enhances the availability of data by distributing copies across multiple nodes. This is especially beneficial for clusters with multiple nodes as it allows for uninterrupted service even if a node becomes unavailable.

4. **Throughput Improvement**: Replication can also increase the throughput of an index. By having multiple replica shards, search queries can be executed on different shards simultaneously, leveraging parallelization and improving performance.

### Replication and Nodes

Replication only makes sense in clusters with multiple nodes. Elasticsearch will only add replica shards for clusters with more than one node. If you configure an index with one or more replicas but have a single node, the replicas will remain unassigned until additional nodes are added to the cluster.

### Replication and Data Loss Prevention

While replication prevents data loss in case of node failures, Elasticsearch also supports taking snapshots for data backups. Snapshots provide a way to export the current state of the cluster or specific indices to a file, allowing restoration to a previous point in time.

Snapshots and replication serve different purposes:

- Replication ensures data availability and prevents loss of live data.
- Snapshots allow you to export the state of the cluster or indices to restore data to a specific point in time, useful for reverting changes or daily backups.

### Exploring Replication with Kibana

In Kibana, we can observe replication-related details.

1. Create a new index using the following command in the Kibana Dev Tools Console:


```bash
PUT /new_index
```

1. Check the cluster health to see if any changes have occurred. The cluster status may change to "yellow" due to the presence of unassigned replica shards.


```bash
GET /_cluster/health
```

1. List the indices to view their status. Newly created indices may have a "yellow" status because replica shards are waiting to be allocated to additional nodes.


```bash
GET /_cat/indices?v
```

1. Use the `_cat` API with the "shards" command to list all the shards in the cluster. This provides information about each shard, including their state and which index they belong to.


```bash
GET /_cat/shards?v
```

   - Primary shards have a state of "STARTED."
   - Replica shards have a state of "UNASSIGNED" until additional nodes are added.

   The presence of unassigned replica shards indicates that the cluster requires more nodes for full replication.

1. Keep in mind that Kibana indices may have specific configurations. The number of shards and replicas may appear as zero, but these values can dynamically change based on the number of nodes in the cluster, ensuring at least one replica for multiple nodes.

Understanding replication and its implications will help you design a robust Elasticsearch cluster that ensures data availability, fault tolerance, and optimal performance.

To add additional nodes to your Elasticsearch cluster, follow these steps:

1. Download the Elasticsearch archive for each additional node you want to add.

2. Extract the archive for each node into separate directories. Do not copy the existing node's directory to ensure a clean start for each additional node.

3. Open the `elasticsearch.yml` file located in the `config` directory of each node's root directory.

4. Uncomment the `node.name` setting and provide a meaningful value for each node to distinguish them easily.

5. Start the enrollment token generation script by running the following command in the terminal, with the working directory set to the root directory of the existing node:

```bash
bin/elasticsearch-create-enrollment-token --scope node
```
Copy the generated enrollment token.

6. Start the additional nodes by running the Elasticsearch script within the `bin` directory of each node's root directory. Provide the enrollment token as an argument. For example:

```bash
bin/elasticsearch --enrollment-token PASTETOKENHERE
```

7. Wait for the new node(s) to start up and join the cluster. The cluster status should transition to "green" once the replica shards are assigned.

8. Verify the distribution of shards across nodes by checking the cluster health and shard allocation. You can use the Cluster Health API and the Shards API to retrieve this information.

9. To simulate a node failure, gracefully shut down the node by pressing CTRL + C or forcefully terminate the process.

10. Monitor the cluster health and shard allocation. Elasticsearch will reassign the unassigned shards to other available nodes after a delay. The cluster status should transition back to "green" once the shard reallocation is complete.

By following these steps, you can add additional nodes to your Elasticsearch cluster and observe how the cluster behaves in terms of shard distribution, fault tolerance, and data availability.

Roles in Elasticsearch determine the behavior and responsibilities of nodes within a cluster. Here's an overview of the different roles and their significance:

1. **Master Role**: The master role makes a node eligible to become the cluster's master node. The master node is responsible for cluster-wide actions, such as managing indices, tracking nodes, and allocating shards. Multiple nodes can have the master role, but only one is elected as the master node through a voting process. Dedicated master nodes are useful for maintaining cluster stability and separating master-related tasks from data-related tasks.

2. **Data Role**: Nodes with the data role store and handle queries related to the cluster's data. By default, most nodes have this role as they store shards. However, in larger and busier clusters, it can be beneficial to have dedicated data nodes and disable the data role for master-eligible nodes to separate master and data responsibilities.

3. **Ingest Role**: The ingest role enables a node to execute ingest pipelines. Ingest pipelines are a series of steps that manipulate documents before they are indexed, similar to Logstash pipelines. Ingest nodes perform data transformations, making them useful for simple transformations when ingesting a high volume of documents. Dedicated ingest nodes can be used for this purpose.

4. **Machine Learning Role**: Nodes with the machine learning (ML) role can run machine learning jobs. The `node.ml` setting identifies a node as an ML node, while the `xpack.ml.enabled` setting enables or disables the node's capability to respond to ML API requests. Dedicated ML nodes separate machine learning tasks from other operations, like search requests.

5. **Coordination Role**: The coordination role is not a specific role but achieved by removing other roles from a node. Coordination nodes are responsible for processing requests and coordinating queries across data nodes. They act as a load balancer for large clusters.

6. **Voting-Only Role**: Nodes with the voting-only role participate in the master election voting process but cannot be elected as the master node themselves. This role is primarily used in large clusters.

In Kibana, you can view the roles of each node in the "node.role" column. The roles are represented by abbreviations. For example, "dim" stands for data, ingest, and master roles.

It's important to note that changing node roles is typically done for large clusters and when there is a need to optimize cluster performance and resource utilization. It's generally recommended to stick with the default roles unless you have a good reason and understanding of the impact. Modifying roles should be done carefully and in conjunction with other optimization techniques such as adjusting shard allocation and cluster scaling.

Remember, understanding node roles is valuable for cluster management and optimization but should be approached cautiously and only implemented when necessary.

To create and delete indices in Elasticsearch, you can use the REST API. Here's an explanation of the process and example code:

1. **Deleting an Index**: To delete an index, use the `DELETE` HTTP verb followed by the index name. In Kibana's Console tool, you can use the following command:

   ```http
   DELETE /pages
   ```

   This example deletes the "pages" index. Remember that a forward slash before the index name is optional but recommended.

2. **Creating an Index**: To create an index, use the `PUT` HTTP verb followed by the index name. You also need to provide index settings using a JSON request body. Here's an example:

   ```http
   PUT /products
   {
     "settings": {
       "number_of_shards": 2,
       "number_of_replicas": 2
     }
   }
   ```

   This example creates an index named "products" with two primary shards and two replica shards. The settings are specified within a nested "settings" object in the JSON request body.

   It's important to note that these shard and replica settings are for demonstration purposes. In production environments, it's recommended to stick to the default values unless you have a specific reason to change them.

After executing these API calls, you will receive a response indicating whether the index operation was successful. The "acknowledged" key indicates if the index was created or deleted, and the "shards_acknowledged" key verifies that the required number of shards were started up within the timeout period.

Remember to exercise caution when deleting indices, as it permanently removes the data associated with them. Additionally, when creating indices, ensure that the index name follows the appropriate naming conventions and reflects the purpose of the data it will store.

With the index created, you can proceed to add documents to it using the various indexing methods available in Elasticsearch.

To index documents in Elasticsearch, you can use the REST API by sending a POST request to the appropriate endpoint. Here's an explanation of the process and example code:

1. **Indexing a Document**: To index a document, use the `POST` HTTP verb followed by the index name, a forward slash, and "_doc." Here's an example:

   ```http
   POST /products/_doc
   {
     "name": "Example Product",
     "price": 19.99,
     "in_stock": true
   }
   ```

   This example adds a document representing a product to the "products" index. The document is defined as a JSON object in the request body, containing fields like "name," "price," and "in_stock."

   The response will include an "_shards" object that indicates the success and failure of storing the document across the shards. The document will be stored on the primary shard and replicated to the replica shards, as defined by the index's configuration.

   Additionally, the response will include an "_id" key, which contains a unique identifier for the document. If an identifier is not specified explicitly, Elasticsearch will generate one automatically.

2. **Specifying Document ID**: To specify a document ID explicitly, change the HTTP verb to `PUT` and append a forward slash followed by the desired ID to the endpoint. Here's an example:

   ```http
   PUT /products/_doc/100
   {
     "name": "Another Product",
     "price": 29.99,
     "in_stock": true
   }
   ```

   This example adds another document to the "products" index with the ID of 100. The document's ID is specified in the request URL, and the JSON object in the request body contains the document's fields.

   In the response, you can observe that the specified ID is reflected in the "_id" key.

   It's important to note that the document ID can be any string value and doesn't have to be an integer as shown in this example.

3. **Auto-Creation of Indices**: Elasticsearch has a setting named "action.auto_create_index" that determines whether indices should be created automatically. By default, this setting is set to "true." If you try to add a document to a non-existing index, Elasticsearch will automatically create the index and then add the document to it. While this behavior can be convenient in development mode, it's generally considered best practice to explicitly create indices.

With the documents indexed, you can proceed to retrieve them using various search and query techniques offered by Elasticsearch.

To retrieve a specific document from Elasticsearch, you can use the REST API and send a GET request to the endpoint that corresponds to the document's ID. Here's an explanation of the process and example code:

1. **Retrieving a Document**: To retrieve a document, use the `GET` HTTP verb and specify the endpoint as the index name, a forward slash, and the document's ID. Here's an example:

   ```http
   GET /products/_doc/100
   ```

   In this example, we retrieve the document with an ID of 100 from the "products" index. The document ID is included in the request URL.

   When executing the query, Elasticsearch will return the document that matches the specified ID. The document's JSON object, which was provided when the document was added, can be found under the "_source" key in the response.

   If the document is not found, the "found" key in the response will be set to "false," and the "_source" key will not be present.

   It's worth noting that in later sections of the course, you will learn about performing searches to retrieve documents that match specific criteria. This allows for more advanced querying capabilities in Elasticsearch.

By utilizing the document's unique ID, you can easily retrieve specific documents from your Elasticsearch index using the GET request.

To update documents in Elasticsearch, you can use the Update API by sending a POST request to the endpoint that corresponds to the document's ID. Here's an explanation of the process and example code:

1. **Updating a Document**: To update a document, use the `POST` HTTP verb and specify the endpoint as the index name, a forward slash, the document's ID, and `_update`. Here's an example:

   ```http
   POST /products/_update/100
   ```

   In this example, we update the document with an ID of 100 from the "products" index. The document ID is included in the request URL, followed by `_update` to indicate the update operation.

   Within the request body, you need to provide a `doc` object containing the fields that you want to update. The keys of the `doc` object correspond to the field names, and the values are the new field values. Here's an example:

   ```json
   {
     "doc": {
       "in_stock": 3
     }
   }
   ```

   In this example, we update the "in_stock" field of the document to 3.

   When executing the update query, Elasticsearch will retrieve the existing document, modify the specified fields according to the `doc` object, and then reindex the document with the same ID. The original document is effectively replaced by the updated version.

   In the response, you will find a key named "result" that indicates the outcome of the update operation. If the document was successfully updated, the value of "result" will be "updated." If the update did not result in any changes (e.g., if you provided the same value as the current field value), the value of "result" will be "noop."

   After updating a document, you can retrieve it again to confirm the changes.

2. **Adding New Fields**: In addition to updating existing fields, you can also add new fields to existing documents using the same update operation. Simply include the new field and its value within the `doc` object. Here's an example:

   ```http
   POST /products/_update/100 
   ```
   ```json
   {
     "doc": {
       "tags": ["tag1", "tag2", "tag3"]
     }
   }
   ```

   In this example, we add a new field named "tags" with an array of string values to the document.

   After the update, you can retrieve the document again to verify that the new field has been added.

   It's important to note that Elasticsearch documents are immutable. When updating a document, the Update API actually retrieves, modifies, and replaces the existing document with the updated version. This process is handled by Elasticsearch to save you from manually retrieving and replacing the document. Additionally, the Update API is more efficient as it reduces the number of network round trips required.

Updating documents in Elasticsearch is a straightforward process that allows you to modify existing fields or add new fields to documents in your index.

To update documents in Elasticsearch using scripts, you can utilize the Update API. Here's an explanation of the process and example code:

1. **Scripted Updates**: Scripted updates allow you to modify document fields without retrieving the current field value. You can perform custom logic using scripts, which can include conditions and other operations. Elasticsearch supports scripting in various languages.

   To use a script for updating a document, you will still use the Update API, but you need to include a "script" object within the request body. The "script" object contains a "source" key, where you provide your script as the value. Here's an example:

   ```http
   POST /products/_update/100
   ```

   ```json
   {
     "script": {
       "source": "ctx._source.in_stock -= params.quantity",
       "params": {
         "quantity": 1
       }
     }
   }
   ```

   In this example, we use a script to decrease the value of the "in_stock" field by one. The script uses the `ctx._source` object to access the document's fields and subtracts the value of `params.quantity` from the "in_stock" field. The `params` object allows you to define dynamic parameters that can be used in your script.

   When executing the script, the document is retrieved, modified, and reindexed with the updated values in a single operation.

   In the response, the "result" key indicates the outcome of the update operation. In this case, the value will be "updated" if the document was successfully updated. If the update did not result in any changes, the value will still be "updated" since scripted updates always trigger an update operation, even if the field values remain the same.

   You can also use the "op" property on the `ctx` variable to explicitly set the operation. For example, setting `ctx.op = "noop"` in the script would result in a "result" value of "noop" if the condition is met.

2. **Deleting Documents**: Scripted updates also allow you to delete documents based on conditions. By setting the `ctx.op` property to "delete" in the script, the document will be deleted. The "result" key in the response will be set to "deleted" to indicate the deletion. Here's an example:

   ```http
   POST /products/_update/100
   ```

   ```json
   {
     "script": {
       "source": "if (ctx._source.in_stock <= 1) { ctx.op = 'delete' }",
       "params": {
         "quantity": 1
       }
     }
   }
   ```

   In this example, if the "in_stock" field is less than or equal to 1, the document will be deleted. Otherwise, no changes will be applied to the document.

   It's worth noting that deleting documents based on conditions using scripting is less common since Elasticsearch provides other mechanisms, such as delete by query, for performing document deletions.

   Please note that scripting is a powerful feature that requires careful consideration, especially in production environments, due to security and performance concerns. It's important to thoroughly understand the implications and potential risks before utilizing scripting in your Elasticsearch deployments.

This concludes the explanation of how to update documents using scripts in Elasticsearch.

Performing upserts in Elasticsearch allows you to conditionally update or insert a document based on its existence. Here's an explanation of upserts and an example of how to use them:

1. **Upserts**: Upserts combine the update and index operations into a single request. If the document already exists, it will be updated using a script. If it doesn't exist, a new document will be indexed with the specified content. This is useful when you want to modify existing documents or add new documents based on certain conditions.

   To perform an upsert, you still use the Update API. The request path remains the same, with the index name and document ID. The script is defined in the request body within the "script" object, and the contents of the "upsert" option represent the new document to be indexed. Here's an example:

   ```http
   POST /products/_update/101
   ```

   ```json
   {
     "script": {
       "source": "ctx._source.in_stock += params.quantity",
       "params": {
         "quantity": 4
       }
     },
     "upsert": {
       "name": "New Product",
       "price": 10.99,
       "in_stock": 4
     }
   }
   ```

   In this example, if a document with an ID of 101 exists, the script will increase the value of the "in_stock" field by 4. If the document doesn't exist, a new document with the specified fields and values will be indexed.

   In the response, the "result" key indicates the outcome of the operation. If the document is updated, the value will be "updated." If a new document is indexed, the value will be "created."

   You can retrieve the document to verify its existence and check if the desired changes were made.

   Upserts can be more complex, involving conditions and dynamic parameters in the script, depending on your specific use case.

This concludes the explanation of performing upserts in Elasticsearch.

**Explanation: Replacing Documents in Elasticsearch**

Replacing documents in Elasticsearch involves indexing a new document with the same ID as an existing document, effectively replacing the entire document. Here's an explanation of document replacement and an example of how to perform it:

1. **Document Replacement**: Document replacement is the process of updating an existing document by indexing a new document with the same ID. It allows you to replace the entire content of a document, including its fields and values.

   To replace a document, you can use the same query that was used for indexing a new document with a specific ID. By providing a new document with the desired fields and values, Elasticsearch will replace the existing document with the new one.

   Let's assume we have an existing document with an ID of 100. Retrieving the current document, we can see its current fields, such as "in_stock" and "tags."

   To replace the document, we can modify any field we want, such as changing the "price" field. By running the query, Elasticsearch will replace the existing document with the new document provided in the query.

   **Request:**

   ```http
   PUT /products/_doc/100
   ```

   ```json
   {
     "name": "Product A",
     "price": 19.99,
     "in_stock": 5
   }
   ```

   By retrieving the replaced document, we can confirm that the old fields have been replaced entirely by the new fields specified in the query.

   It's important to note that when performing a document replacement, the entire document is replaced, including any fields that were not specified in the new document. Therefore, if a field is missing in the new document, it will be removed from the replaced document.

This concludes the explanation of replacing documents in Elasticsearch.

**Explanation: Deleting Documents in Elasticsearch**

Deleting documents in Elasticsearch is a straightforward process. Here's an explanation of how to delete documents and an example of performing a document deletion:

1. **Deleting Documents**: To delete a document in Elasticsearch, you need to send a DELETE request to the endpoint that specifies the document's ID. The REST API's simplicity and intuitive design make the process of deleting documents straightforward.

   Just like when retrieving a document, you can use the query to retrieve a document as a starting point. However, instead of retrieving the document, you change the HTTP verb from GET to DELETE. This tells Elasticsearch to remove the document associated with the specified ID.

   Let's take an example where we want to delete a document with the ID of 100. By running the DELETE request, Elasticsearch will delete the document with that ID.

   **Request:**

   ```http
   DELETE /products/_doc/100
   ```

   After executing the query, the document is deleted, and subsequent attempts to retrieve the document will result in a "document not found" response.

   Deleting a document using the DELETE request removes it entirely from the Elasticsearch index, and it will no longer be available for search or retrieval.

   It's worth mentioning that Elasticsearch also provides the ability to delete documents based on specific criteria using query-based deletions. This allows you to delete multiple documents that match certain conditions, which we will cover later in the course.

This wraps up the explanation of deleting documents in Elasticsearch.

**Explanation: Routing in Elasticsearch**

Routing is a fundamental concept in Elasticsearch that determines how documents are allocated to shards and how they can be located or accessed. Here's an explanation of routing in Elasticsearch and how it works:

1. **Resolving Document Shards**: When indexing a new document, updating an existing document, or performing operations like retrieval, updating, or deletion based on document IDs, Elasticsearch uses a routing formula to determine which shard contains or should contain the document.

   By default, the routing formula is based on the document's ID. Elasticsearch calculates the shard number using a simple formula: `shard_number = hash(_routing) % number_of_primary_shards`. The `_routing` value defaults to the document's ID.

   This routing formula ensures that Elasticsearch can efficiently locate and store documents based on their IDs. When performing operations like retrieval, update, or deletion, Elasticsearch uses the same formula to determine the shard that contains the document.

2. **Even Shard Distribution**: The default routing strategy in Elasticsearch has another advantage—it ensures that documents are evenly distributed across the shards within an index. This balanced distribution helps maintain optimal performance and prevents one shard from storing significantly more documents than others.

   If you were to change the default routing strategy, you would need to ensure that documents are distributed evenly across shards manually. Failing to do so may result in uneven storage and retrieval patterns, affecting search performance.

3. **Metadata Fields**: When indexing documents, Elasticsearch stores metadata along with the document's contents. The document itself is stored within the `_source` field, while the document's identifier (ID) is stored in the `_id` field. Another meta field related to routing is the `_routing` field, which you saw in the routing formula. The `_routing` field is only present in the query results if a custom routing value is specified during document indexing.

   The metadata fields in Elasticsearch provide essential information for document management and retrieval operations.

4. **Implications of Changing Shard Count**: It's important to note that once an index is created, the number of shards cannot be changed. The routing formula includes the number of shards as a variable, which means that changing the shard count would yield different routing results. This would cause issues when locating existing documents based on their IDs.

   Suppose you indexed a document with a routing formula that resulted in shard number 2. If you were to increase the number of shards in the index, retrieving documents based on their IDs might fail because the routing formula would yield different results. Elasticsearch would attempt to locate the document on the wrong shard, resulting in an empty response.

   Additionally, changing the shard count could lead to uneven document distribution across shards, which can impact performance. Modifying the number of shards requires creating a new index and reindexing the documents into it.

These are the key aspects of routing in Elasticsearch. The default routing strategy simplifies document management and retrieval while ensuring even distribution across shards. Understanding routing is crucial for efficient document storage and retrieval in Elasticsearch.

Sure! Here's a simplified diagram explaining the process of reading data in Elasticsearch:

```
                              +---------+
                              |  Client |
                              +----+----+
                                   |
                                   | Read Request
                                   |
                              +----v----+
                              |Coordinating|
                              |   Node    |
                              +----+----+
                                   |
                            Routing Resolution
                                   |
                              +----v----+
                              |Primary   |
                        +---->|Shard     |
                        |     +----+----+
                        |          |
                  Shard Selection   |
                        |          |
                        |     +----v----+
                        |     | Shard    |
                        |     | Replica  |
                        |     +----+----+
                        |          |
                        |   Read Response
                        |          |
                  +-----+----+     |
                  |Coordinating|    |
                  |   Node     |    |
                  +-----+----+     |
                        |          |
                        |   Response Sent
                        |          |
                   +----v-----+     |
                   |  Client  |     |
                   +----------+     |
```

This diagram illustrates the flow of reading data in Elasticsearch:

1. The client initiates a read request, which is received by the coordinating node.
2. The coordinating node determines the shard where the requested document is stored through routing.
3. Instead of directly accessing the primary shard, Elasticsearch uses Adaptive Replica Selection (ARS) to select an optimal shard replica based on various factors.
4. The coordinating node sends the read request to the selected shard replica.
5. The shard replica processes the request and retrieves the requested document.
6. The coordinating node collects the response from the shard replica.
7. The response is sent back to the client, which receives and handles the retrieved data.

This process ensures efficient and distributed retrieval of data in Elasticsearch, enabling scalability and improved query performance.

```
                                   +---------+
                                   |  Client |
                                   +----+----+
                                        |
                                        | Write Request
                                        |
                                   +----v----+
                                   |Coordinating|
                                   |   Node    |
                                   +----+----+
                                        |
                                 Routing Resolution
                                        |
                                   +----v----+
                                   |Primary   |
                             +---->|Shard     |
                             |     +----+----+
                             |          |
                       Request Validation
                             |          |
                       +----v----+     |
                       |Primary   |     |
                       |Shard     |     |
                       +----+----+     |
                            |          |
                       Write Operation  |
                            |          |
                            |     +----v----+
                            |     | Shard    |
                            |     | Replica  |
                            |     +----+----+
                            |          |
                       Replication      |
                            |          |
                            |     +----v----+
                            |     | Shard    |
                            |     | Replica  |
                            |     +----+----+
                            |          |
                       Write Response   |
                            |          |
                       +----v-----+     |
                       |Coordinating|    |
                       |   Node     |    |
                       +-----+----+     |
                             |          |
                       Response Sent     |
                             |          |
                        +----v-----+     |
                        |  Client  |     |
                        +----------+     |
```

This diagram illustrates the flow of writing data in Elasticsearch:

1. The client initiates a write request, which is received by the coordinating node.
2. The coordinating node determines the replication group where the document should be stored through routing.
3. The write request is resolved to the primary shard responsible for the replication group.
4. The primary shard validates the request, ensuring the operation's structure and field values are correct.
5. The primary shard performs the write operation locally and forwards it to the replica shards within the replication group.
6. The replica shards receive the operation in parallel to keep them up to date.
7. The primary shard generates a write response.
8. The coordinating node collects the response from the primary shard.
9. The response is sent back to the client, which receives confirmation of the successful write operation.

This process ensures that write operations are coordinated through the primary shard and replicated to the replica shards for data consistency and fault tolerance. Elasticsearch utilizes primary terms, sequence numbers, and checkpoints to handle failures and maintain data integrity during replication.

Note: The diagram represents a simplified overview of the write process in Elasticsearch and omits certain details for clarity.

1. The client sends a write request, which is received by the coordinating node.
2. The coordinating node resolves the request through routing to the primary shard responsible for the document.
3. The primary shard validates the request, ensuring the structure and field values are correct.
4. The primary shard performs the write operation locally and forwards it to the replica shards for replication.
5. The replica shards receive the operation and apply it to keep the data consistent.
6. The primary shard generates a write response.
7. The coordinating node collects the response from the primary shard.
8. The response is sent back to the client, confirming the successful write operation.

During this process, Elasticsearch maintains a metadata field called "_version" for each document. The "_version" field starts at 1 and is incremented every time the document is updated or deleted. If a document is deleted, Elasticsearch retains the version number for 60 seconds by default. If a new document with the same ID is indexed within that time, the version number is incremented; otherwise, it is reset to 1.

The versioning mechanism in Elasticsearch provides basic information about the number of times a document has been modified. However, it is generally not used for optimistic concurrency control, as it has been superseded by primary terms and sequence numbers.

Note: The diagram represents a simplified overview of the versioning process in Elasticsearch and omits certain details for clarity.

### Optimistic Concurrency Control in Elasticsearch

Sure! Here's a simplified explanation of how you can achieve optimistic concurrency control in Elasticsearch:

#### What is Optimistic Concurrency Control?

Optimistic concurrency control is a technique used to handle concurrent write operations on the same document without blocking or locking the document. It allows multiple clients to attempt writes concurrently and resolves conflicts when conflicts occur.

In Elasticsearch, optimistic concurrency control can be achieved using the `_version` metadata field and the concept of retries.

#### How Optimistic Concurrency Control Works

1. When indexing or updating a document, the client includes the current `_version` value in the request.

2. The coordinating node receives the write request and forwards it to the primary shard responsible for the document.

3. The primary shard compares the `_version` value in the request with the current `_version` of the document.

4. If the `_version` values match, the primary shard applies the write operation and increments the `_version` of the document by one.

5. If the `_version` values don't match, it means another write operation has modified the document in the meantime. The primary shard returns a version conflict error to the client.

6. Upon receiving a version conflict error, the client can choose to retry the write operation with the updated document and the new `_version` value.

#### Diagram: Optimistic Concurrency Control in Elasticsearch

Here's a simplified diagram illustrating the process of optimistic concurrency control in Elasticsearch:
```plaintext
  +-----------------+           +---------------+           +-----------------+
  |                 |           |               |           |                 |
  |    Client       |           |  Coordinating |           |   Primary Shard |
  |                 |           |     Node      |           |                 |
  |                 |           |               |           |                 |
  +--------+--------+           +-------+-------+           +--------+--------+
           |                           |                            |
           |  Index/Update Document     |                            |
           +-------------------------->|                            |
           |                           |  Compare _version          |
           |                           +-------------------------->|
           |                           |                            |
           |                           |  Versions match            |
           |                           |<---------------------------+
           |                           |                            |
           |  Apply Write Operation    |                            |
           |                           |                            |
           |                           |  Increment _version        |
           |                           |--------------------------->|
           |                           |                            |
           |                           |  Return success response   |
           |                           |<---------------------------+
           |                           |                            |
           |                           |                            |
           |                           |                            |
```

This diagram represents the steps involved in achieving optimistic concurrency control:

1. The client sends a write request with the current `_version` value.
2. The coordinating node routes the request to the primary shard responsible for the document.
3. The primary shard compares the `_version` in the request with the current `_version` of the document.
4. If the `_version` matches, the primary shard applies the write operation and increments the `_version`.
5. If the `_version` doesn't match, a version conflict error is returned to the client.
6. The client can retry the write operation with the updated document and the new `_version`.

Note: The diagram provides a simplified representation of the optimistic concurrency control process and excludes some implementation details for clarity.

#### Example Code: Optimistic Concurrency Control

Here's an example of how you can implement optimistic concurrency control in Elasticsearch using the Python Elasticsearch library:

```python
from elasticsearch import Elasticsearch

# Create an Elasticsearch client
es = Elasticsearch()

# Document ID and initial version
doc_id = 'your_document_id'
current_version = 1

# Prepare the document to be indexed or updated
document = {
    'title': 'Your Document Title',
    'content': 'Your Document Content',
    '_version': current_version  # Include the current version in the document
}

# Index or update the document with versioning
try:
    # Index or update the document with the specified ID and version
    response = es.index(index='your_index', id=doc_id, body=document, version=current_version)

    # If the operation succeeds, retrieve the updated version
    updated_version = response['_version']
    print(f"Document '{doc_id}' has been indexed/updated with version: {updated_version}")
except Exception as e:
    # Handle version conflict error
    print(f"Version conflict occurred for document '{doc_id}': {e}")
```

In the code example above:

1. We create an Elasticsearch client using the Python Elasticsearch library.
2. We define the document ID and the current version of the document.
3. The document to be indexed or updated includes the current version in the `_version` field.
4. We use the `index` method of the Elasticsearch client to perform the indexing or updating operation, specifying the document ID, index name, and the current version.
5. If the operation succeeds, the updated version of the document is retrieved from the response.
6. In case of a version conflict error, an exception is raised and can be handled accordingly.

Please note that the code example assumes you have the Python Elasticsearch library installed and have a running Elasticsearch cluster.

Keep in mind that optimistic concurrency control is just one approach to handle concurrent writes, and it may not be suitable for every use case. Other techniques, such as pessimistic locking, may be more appropriate in certain scenarios.

### Optimistic Concurrency Control with Elasticsearch

In this lecture, we will explore the concept of optimistic concurrency control in Elasticsearch. This technique helps prevent conflicts when multiple write operations are performed on the same document out of sequence. We'll discuss how versioning can be used to address this issue.

#### The Problem with Concurrent Updates

Consider an example of an e-commerce application where multiple threads or processes may update the same product concurrently. Suppose two threads retrieve the product simultaneously and attempt to decrement the "in_stock" field. If both threads update the product without knowledge of each other, inconsistencies can arise.

#### The Old Approach: Using "_version" Field

Previously, the "_version" field was used for versioning in Elasticsearch. When retrieving a document, the current version was returned. Subsequently, the version was sent along with the update request. If the supplied version did not match the stored version, the update operation would fail.

#### The New Approach: Primary Terms and Sequence Numbers

To overcome the limitations of the old approach, Elasticsearch introduced primary terms and sequence numbers. These features offer a more robust solution for optimistic concurrency control.

#### Retrieving the Document and Obtaining Primary Terms and Sequence Numbers

When retrieving a document, the primary term and sequence number are included in the response. These metadata fields provide information about the document's current state.

```plaintext
GET /my_index/_doc/1

Response:
{
  "_index": "my_index",
  "_type": "_doc",
  "_id": "1",
  "_version": 5,
  "_primary_term": 2,
  "_seq_no": 17,
  "_source": {
    "product_name": "Example Product",
    "in_stock": 10
  }
}
```

#### Updating the Document with Primary Terms and Sequence Numbers

To ensure safe updates, the primary term and sequence number can be included as query parameters when sending an update request.

```plaintext
POST /my_index/_doc/1/_update?if_seq_no=17&if_primary_term=2
{
  "doc": {
    "in_stock": 9
  }
}
```

Elasticsearch will validate the supplied primary term and sequence number against the current values stored in the index. If they match, the update operation will proceed. Otherwise, an error will be returned.

#### Handling Concurrency Conflicts

In case of a concurrency conflict, where the document has been updated by another process or thread since retrieval, the update operation will fail. In such scenarios, it's essential to handle the error within your application. This typically involves re-retrieving the document, obtaining the new primary term and sequence number, and reattempting the update. Remember to consider any changes in field values that might have occurred during the process.

#### Conclusion

Optimistic concurrency control with primary terms and sequence numbers provides a reliable mechanism to handle concurrent updates in Elasticsearch. While not necessary for all use cases, it is crucial in scenarios where multiple processes or threads may modify the same document simultaneously.

### Updating Multiple Documents with a Query

In this lecture, we will learn how to update multiple documents in Elasticsearch using a query. This functionality is similar to the UPDATE query in relational databases, allowing us to apply updates based on specific conditions.

#### Introduction to Updating Multiple Documents

When dealing with multiple documents, it's more efficient to update them in a single query rather than individually. Elasticsearch provides the Update By Query API to accomplish this task. However, understanding primary terms, sequence numbers, and optimistic concurrency control is essential for comprehending the internal workings of this query.

#### Example Scenario: Updating "in_stock" Field

Let's assume we want to reduce the "in_stock" field value by one for each product in a purchase. To achieve this, we'll use the Update By Query API and a simple search query to update all documents.

#### Constructing the Update By Query Request

To begin, we'll define the HTTP verb and request path for the Update By Query API. Next, we'll specify the script within the request body, similar to updating a single document with a script.

```plaintext
POST /product/_update_by_query
{
  "script": {
    "source": "ctx._source.Otherdata--"
  },
  "query": {
    "match_all": {}
  }
}
```

In the example above, we use a simple script to decrement the "in_stock" field by the specified quantity. The query section defines the search query, which currently matches all documents.

#### Understanding the Update By Query Process

The Update By Query API works by creating a snapshot of the index and then performing a search query on each shard to identify matching documents. If any documents match the query, a bulk request is sent to update them.

The results of the Update By Query request provide additional information about the query execution. The "batches" field indicates the number of batches used to retrieve and update documents. The Scroll API is used internally to handle large result sets efficiently.

Errors that occur during the search query or bulk request are automatically retried up to ten times. If the retries are unsuccessful, the entire query is aborted. The failures are reported in the results under the "failures" key.

#### Version Conflicts and Aborted Queries

During the update process, Elasticsearch uses the snapshot's primary terms and sequence numbers to ensure consistency. If a document has changed since the snapshot was taken, a version conflict occurs, and the document is not updated. This also results in the query being aborted.

The number of version conflicts can be found under the "version_conflicts" field in the query results. By default, a version conflict causes the entire query to be aborted. However, you can specify the "conflicts" parameter with a value of "proceed" to allow the query to continue despite conflicts:

```plaintext
POST /product/_update_by_query
{
  "conflicts": "proceed"
  "script": {
    "source": "ctx._source.Otherdata--"
  },
  "query": {
    "match_all": {}
  }
}
```

#### Verifying the Updates

To verify the updates, we can perform a simple search query matching all documents. In this example, we assume the "in_stock" field values have been updated correctly.

```plaintext
GET /my_index/_search
{
  "query": {
    "match_all": {}
  }
}
```

Upon inspecting the results, we can confirm that the "in_stock" field values have been decremented as expected.

#### Conclusion

Updating multiple documents in Elasticsearch using the Update By Query API allows for efficient and condition-based updates. By understanding the internal workings of this process, including version conflicts and query aborts, you can handle updates with confidence while ensuring data consistency.

To delete documents based on a condition, we can use the Delete By Query API. This allows us to remove documents that match a specified search query. Let's dive into the details:

```plaintext
POST /products/_delete_by_query
{
  "query": {
    "match_all": {}
  }
}
```

In this example, we are deleting all documents within the "products" index. The query section specifies the search query used to identify the documents for deletion. In this case, the "match_all" query matches all documents in the index.

After executing the query, the response will indicate the number of deleted documents. In our case, we can see that two documents were successfully deleted.

Similar to the Update By Query API, the Delete By Query API handles errors, performs operations in batches, and utilizes primary terms and sequence numbers. You can also include the "conflicts" parameter with a value of "proceed" to ignore version conflicts, as discussed in the previous lecture.

That's all there is to deleting documents based on a condition using the Delete By Query API. It provides a powerful way to remove multiple documents that meet specific criteria.

We started out indexing, updating, and deleting individual documents. Then we covered how to update and delete multiple documents at once, based on a condition that we defined.

In this lecture, I am going to show you how we can index, update, or delete many documents at once - potentially thousands at a time. We can do this by processing individual requests in batches; specifically by using the Bulk API.

This API accepts a number of lines, each separated by a newline character, being either `\n` or `\r\n`. In a text editor, this just means that you will have to add a line break at the end of each line, i.e., hitting the Enter key. Each of these lines should be a JSON object. This format is based on a specification called NDJSON.

Let's demonstrate how to perform different actions in a single bulk request using the Bulk API. We will use examples for indexing, updating, creating, and deleting documents.

First, let's index a new document:

```plaintext
POST /_bulk

{"index":{"_index":"products","_id":"200"}}
{"field1":"value1","field2":"value2","field3":"value3"}
```

With this code, we are instructing Elasticsearch to index a new document in the "products" index with an ID of 200. The document contains the fields "field1," "field2," and "field3" with their respective values.

Next, let's update a document:

```plaintext
POST /_bulk

{"update":{"_index":"products","_id":"201"}}
{"doc":{"field1":"updated value1"}}
```

In this example, we are performing an update operation on an existing document in the "products" index with an ID of 201. We specify the "update" action and provide the updated field value in the "doc" object.

Now, let's create a new document:

```plaintext
POST /_bulk

{"create":{"_index":"products","_id":"202"}}
{"field1":"value4","field2":"value5","field3":"value6"}
```

With this code, we are instructing Elasticsearch to create a new document in the "products" index with an ID of 202. The document contains the fields "field1," "field2," and "field3" with their respective values.

Lastly, let's delete a document:

```plaintext
POST /_bulk

{"delete":{"_index":"products","_id":"203"}}
```

In this example, we are performing a delete operation on an existing document in the "products" index with an ID of 203. We specify the "delete" action, and Elasticsearch will remove the corresponding document.

When running the bulk request, Elasticsearch will process each line as an individual action. In this case, it will index a new document, update an existing document, create a new document, and delete a document. The response will contain information about the success or failure of each action.

That's how you can perform indexing, updating, creating, and deleting of multiple documents using the Bulk API in Elasticsearch. You can include different actions in a single bulk request to perform various operations simultaneously.

Now that you know how to use the Bulk API, let's use it from the command line to import some test data that we will be using throughout the course.

To do this, we will use an HTTP client called cURL, which is the most popular command-line tool for sending HTTP requests. If you are using macOS or Linux, you should already have it installed. The same applies to some Windows installations, so you might not have to install it yourself. If it's not available on your system, you can download it from the cURL website.

First, download the file containing the test data. You can find the file attached to this lecture or within the GitHub repository. Open the file in a text editor to see its contents.

As you can see, the file contains a series of "index" actions, 1000 in total. Each document has been assigned a sequential ID. Since the index name is not specified within the action metadata, we need to specify it in the request itself, specifically within the request path.

Before importing the data, ensure that the file ends with a newline character. In a text editor, this means the last line of the file should be empty.

Now, let's construct the command to send an HTTP request to the Bulk API. Open a terminal window and set the working directory to the location of the downloaded file.

The cURL command starts with `curl`. We need to specify the `Content-Type` header using the `-H` option, which should be set to the NDJSON content type.

Next, we specify the HTTP verb. By default, cURL uses "GET," but for the Bulk API, we need to use "POST." Use the `-X` option to specify the verb.

Following the HTTP verb, enter the URL to the Bulk API. Since we are not using the Console tool, provide the fully qualified URL, such as `http://localhost:9200`.

If you want the response to be formatted for readability, you can include the `pretty` query parameter without any value. This is optional and mainly useful for human inspection.

Finally, we need to send the data file along with the POST request. Use the `--data-binary` option and specify the file name in double quotes, preceded by the `@` symbol. This tells cURL that the value is a file name, not a path.

Here is an example of the command:

```plaintext
curl -H "Content-Type: application/x-ndjson" -X POST "http://localhost:9200/_bulk?pretty" --data-binary "@data-file.json"
```

Replace `data-file.json` with the actual name of your data file.

When you run the command, Elasticsearch will process the bulk request and respond with a result set, similar to what you saw in the previous lecture. If you are running the bulk request within a script, you can process the results accordingly. In this case, we are interested in the successful import of the data.

Note that if your index already contains documents with the same IDs as those in the bulk request, the existing documents will be replaced. If you used the "create" action instead, some actions may fail due to conflicts.

To verify the distribution of the imported documents across the shards in your Elasticsearch cluster, you can run a query to inspect the shards. This query should return information about the distribution of the documents.

That's it! Now you have successfully imported test data using the Bulk API and cURL from the command line. You can now proceed with working on the data throughout the course.

Sometimes this may not work, hence you may need to make changes like so
```bash
    curl -u elastic --cacert config/certs/ca.crt -H "Content-Type: application/x-ndjson"-X POST "https://localhost:9200/_bulk?pretty" --data-binary "@data-file.json"
```

The first topic we will cover is analysis, also known as text analysis. Analysis is specifically applicable to text values. When we index a text value, it goes through an analysis process to store the values in a data structure optimized for searching.

In the previous section, when we retrieved documents, the indexed values were returned under the "_source" key. However, these values are not used internally by Elasticsearch when determining document matches for search queries. Text values need to be processed before they can be efficiently searched.

During the indexing process, a text value is analyzed using an analyzer. An analyzer consists of three components: character filters, a tokenizer, and token filters. The result of analyzing text values is stored in a searchable data structure.

Let's examine each component of the analyzer:

1. Character Filters: Character filters receive the original text and can modify it by adding, removing, or changing characters. An analyzer may have zero or more character filters, which are applied in the specified order. For example, the "html_strip" character filter can remove HTML elements and convert HTML entities.

2. Tokenizer: An analyzer must have exactly one tokenizer, which is responsible for tokenizing the text. Tokenizing refers to splitting the text into tokens, often by removing punctuation and splitting on whitespace. For instance, a tokenizer can split a sentence into words based on whitespace. The tokenizer also records the character offsets for each token in the original string.

3. Token Filters: Token filters receive the tokens produced by the tokenizer and can add, remove, or modify tokens. Similar to character filters, an analyzer may have zero or more token filters that are applied in the specified order. A simple example is the "lowercase" filter, which converts all letters to lowercase.

Elasticsearch provides built-in character filters, tokenizers, and token filters that can be combined to create custom analyzers. In this section, we will focus on the default behavior, but we will explore custom analyzers later.

By default, Elasticsearch uses the "standard" analyzer for all "text" fields unless otherwise configured. This analyzer does not apply any character filter, passes the text to the tokenizer, which uses the Unicode Segmentation algorithm to split the text into tokens based on whitespace and punctuation. Finally, the tokens are passed through the "lowercase" token filter to convert all letters to lowercase.

In addition to the "standard" analyzer, there are other analyzers available, but the "standard" analyzer is the most commonly used. Later in this section, I will provide an overview of the important analyzers, character filters, tokenizers, and token filters.

For now, it's essential to understand the purpose of analyzers and the behavior of the "standard" analyzer.

In the previous lecture, we learned about analysis in Elasticsearch and the "standard" analyzer. Now, let's explore an API that allows us to test how Elasticsearch analyzes a given string.

To test the "standard" analyzer, we can use the "_analyze" endpoint with the HTTP verb set to POST. We provide the text we want to analyze as a parameter named "text." For example, let's say we have a text string containing a joke:

```bash
POST /_analyze
{
  "text": "Why don't scientists trust atoms? Because they make up everything!"
}
```

This query will analyze the given text using the "standard" analyzer, which is the default behavior if we don't specify a different analyzer.

When we run this query, Elasticsearch will process the text using the "standard" analyzer and return the tokens generated during the analysis. Tokens are the individual units of text after the analysis process. They can be thought of as the "building blocks" that Elasticsearch uses to understand and search text.

The result of the analysis will include the tokens and their associated metadata. Each token has a type, which is usually alphanumeric and represents the type of the token. For example, a number token would have a numeric type.

The result also includes the start and end offsets for each token. These offsets represent the character positions of the token within the original text before analysis. They can be useful for highlighting search results later on.

Let's take a look at an example result:

```json
{
  "tokens": [
    {
      "token": "why",
      "start_offset": 0,
      "end_offset": 3,
      "type": "<ALPHANUM>",
      "position": 0
    },
    {
      "token": "don't",
      "start_offset": 4,
      "end_offset": 9,
      "type": "<ALPHANUM>",
      "position": 1
    },
    {
      "token": "scientists",
      "start_offset": 10,
      "end_offset": 20,
      "type": "<ALPHANUM>",
      "position": 2
    },
    ...
  ]
}
```

In this example, the joke has been tokenized into individual words, and each token represents a word in the joke. The start_offset and end_offset indicate the character positions of each word within the original text. The type of each token is "<ALPHANUM>", indicating that it contains alphanumeric characters.

By inspecting the tokens, we can observe how the "standard" analyzer processes the text. It splits the text into words, removes punctuation marks, and converts words to lowercase.

It's important to note that the "_analyze" API allows us to understand how Elasticsearch interprets and breaks down text. This knowledge can be useful when building custom analyzers or when trying to understand the behavior of different analyzers available in Elasticsearch.

In the next lecture, we will explore what happens with the tokens generated by an analyzer and how they are stored and used by Elasticsearch.

Alright, let's understand what happens with the tokens generated during analysis in Elasticsearch. To store field values efficiently, Elasticsearch uses different data structures depending on the field's data type and access patterns. In this lecture, we'll focus on one specific data structure called an inverted index.

An inverted index is a mapping between terms and the documents that contain those terms. Terms refer to the tokens generated by the analyzer during the analysis process. Essentially, an inverted index allows us to quickly find which documents contain a specific term.

Let's take an example to see how the inverted index is constructed. Suppose we have a single document with the following text: "Elasticsearch is powerful and easy to use." Each unique term in the document is indexed and associated with the document ID.

The inverted index would look like this:

```
Term     | Document IDs
-----------------------
Elasticsearch | 1
is             | 1
powerful       | 1
and            | 1
easy           | 1
to             | 1
use            | 1
```

Notice that the terms are sorted alphabetically for efficient searching. In this example, each term appears only in one document.

Now, let's index a few more documents and see how the inverted index grows:

```
Term     | Document IDs
-----------------------
Elasticsearch | 1, 2
is             | 1, 3
powerful       | 1
and            | 1, 2
easy           | 1, 2
to             | 1, 2, 3
use            | 1, 3
search         | 2, 3
```

As more documents are indexed, the inverted index expands accordingly. Each term is associated with the document IDs in which it appears.

The inverted index allows for efficient term-based searching. For example, if we search for the term "easy," Elasticsearch can quickly look up the inverted index to find the documents that contain that term, which in this case are documents 1 and 2.

It's worth noting that an inverted index is named as such because the logical mapping would be from documents to the terms they contain. However, for efficient searching, the relationship is inverted, meaning terms are mapped to the documents containing them.

The inverted index we discussed is a simplified representation. In reality, the inverted index within Apache Lucene (the underlying engine of Elasticsearch) contains additional information, such as data used for relevance scoring. Relevance scoring is a topic we'll cover in a later part of the course.

Now that you understand the basics of an inverted index, let's address a common question: What happens when we have multiple fields with different data types? Each text field has its own inverted index, meaning that an inverted index is created per text field. For example, if we have fields like "name" and "description," we'll have separate inverted indices for each field.

The inverted index plays a crucial role in full-text searching and efficiently retrieving documents containing specific terms. Elasticsearch leverages other data structures like BKD trees for numeric, date, and geospatial fields to handle different access patterns.

To summarize, an inverted index is a sorted mapping between terms and the documents containing those terms. It enables efficient term-based searching. Elasticsearch utilizes inverted indices for text fields, while other data structures are used for fields with different data types.

Now that we have a good understanding of text analysis and the storage of terms, let's dive into mapping in Elasticsearch. Mapping defines the structure of documents, including their fields and data types. In a way, you can think of mapping as similar to a table schema in a relational database.

To illustrate the concept, let's consider a simple table in a relational database. On your screen, you can see an example of how this table could be mapped in Elasticsearch. The mapping defines the fields (e.g., "name," "age," "email") and their respective data types (e.g., "text," "integer," "keyword").

However, mapping in Elasticsearch goes beyond just defining fields and data types. It offers more flexibility and functionality. So, let's explore the two basic approaches to mapping in Elasticsearch: explicit mapping and dynamic mapping.

With explicit mapping, we define the fields and their data types ourselves, typically when creating an index. This means we explicitly specify the fields and their properties, such as whether they are searchable, aggregatable, or stored. Explicit mapping gives us fine-grained control over the mapping configuration.

On the other hand, Elasticsearch also supports dynamic mapping. When Elasticsearch encounters a new field that hasn't been explicitly mapped, it automatically creates a field mapping based on the value it receives. For example, if Elasticsearch encounters a string value, it will use the "text" data type for the mapping. Dynamic mapping makes it easier to get started with Elasticsearch because it automatically infers the mapping based on the data.

It's important to note that explicit and dynamic mapping can be combined. This means we can have some fields explicitly mapped while allowing Elasticsearch to dynamically map others based on the incoming data. This flexibility allows us to adapt the mapping to different scenarios.

Now that we have a brief introduction to mapping, we can start exploring and defining our mappings in Elasticsearch. Mapping is a powerful feature that helps Elasticsearch understand the structure of our documents and how to index and store them effectively.

Now that we have covered the basics of mapping, let's take a closer look at the available data types in Elasticsearch. While there are several data types, I will highlight the most important ones.

On your screen, you can see some of the basic data types in Elasticsearch. Many of these data types are familiar, as they are commonly used in programming languages. For example, we have "text" for full-text search, "keyword" for exact value matching, "integer" for whole numbers, "float" for decimal numbers, "date" for date and time values, and "boolean" for true/false values.

In addition to these basic data types, Elasticsearch also offers more specialized data types for specific use cases. For example, there is an "ip" data type for storing IP addresses, "geo_point" for geolocation data, and "completion" for auto-completion functionality. These specialized data types cater to specific Elasticsearch features and will be introduced throughout the course as they become relevant.

I encourage you to explore the documentation to see the full list of data types available in Elasticsearch. There are some interesting data types that are useful for specific use cases but may not be covered in this course.

Now let's delve into a more complex data type called the "object" data type. The "object" data type represents a JSON object. In Elasticsearch, each indexed document is a JSON object that can contain fields with object values. These objects can also have nested objects, creating an object hierarchy.

To define an object in the mapping, we use the "properties" key instead of the usual "type" key. Within the "properties" key, we define the keys that the object contains. The same syntax applies to fields at the root level of the mapping.

Although we define objects as regular JSON objects when indexing documents, Elasticsearch internally flattens the objects to a format compatible with Apache Lucene, which is the underlying technology. This allows Elasticsearch to index any document that is valid according to the JSON specification. The flattened objects are stored within Lucene, and we can still query them using dot notation syntax.

If we try to index an array of objects, the objects are flattened in a similar manner. The values are grouped by field name and indexed as an array. This means that a search query against a field will search through all the values within the array. While this can be useful in certain scenarios, it can also cause challenges when maintaining relationships between object values.

To address this, Elasticsearch provides a specialized data type called "nested." The "nested" data type maintains the relationship between object values when an array of objects is indexed. With "nested" data type, we can query objects independently, ensuring that the object values are not mixed together. This is achieved by using specific queries designed for nested objects.

Another data type worth mentioning is the "keyword" data type. The "keyword" data type is used for fields where exact value matching is required. It is suitable for filtering, sorting, and aggregating documents. For example, if we have a "status" field for news articles, we can use the "keyword" data type to search for articles with a specific status value, such as "published." If we need to perform full-text searches that don't require exact matches, we would use the "text" data type instead.

This gives you a brief overview of the most important data types in Elasticsearch. Remember to refer to the documentation for a comprehensive list of data types available in Elasticsearch.

In the previous lecture, we discussed the use case for the "keyword" data type, which is primarily focused on filtering, sorting, and aggregations. However, why is its use limited to these purposes? Why can't we use it for full-text searches like the "text" data type?

To answer these questions, we need to understand how "keyword" fields are analyzed and stored in Elasticsearch. While the "text" fields use the "standard" analyzer, the "keyword" fields use a specific analyzer called the "keyword" analyzer.

The "keyword" analyzer is a no-op analyzer, meaning it doesn't modify the input string in any way. It returns the unmodified input string as a single token. This is because "keyword" fields are intended for exact matching. We can verify this by using the Analyze API, which allows us to see how the input string is analyzed.

When we analyze a value with the "keyword" analyzer, we can observe that the string is left entirely untouched and is returned as a single token. No symbols are stripped out, and letters are not converted to lowercase. This preservation of the original value is crucial for exact matching because any modification to the string would result in a mismatch between the indexed value and the search query.

Looking at the inverted index for "keyword" fields, we can see that the entire field values are stored as a single term. Unlike "text" fields where tokenization and analysis take place, "keyword" fields maintain the original string as is.

While the example we saw used sentences for demonstration purposes, a more realistic use case for "keyword" fields would be to map data such as email addresses or article statuses. These are values where exact matches are typically required.

It's worth noting that although the "keyword" analyzer is a no-op analyzer, we can still customize analyzers, including the "keyword" analyzer. For instance, we can configure the "keyword" analyzer to include the "lowercase" token filter, which would lowercase the letters in the indexed value. However, this modification should be done cautiously and only when it aligns with the specific use case.

In summary, fields that use the "keyword" data type are analyzed using the "keyword" analyzer, which essentially keeps the input string intact and treats it as a single token. The original value is stored as a term in the inverted index, making the "keyword" data type suitable for exact matching and structured data such as email addresses, order statuses, and product tags.

In Elasticsearch, type coercion refers to the ability of Elasticsearch to convert field values to the appropriate data type during the indexing process. Let's go through the concept of type coercion with step-by-step examples.

1. Indexing a Document with a Floating-Point Number:
   - We run a query to index a document with a floating-point number for the "price" field.
   - Elasticsearch inspects the value and determines its data type to be "float" based on dynamic mapping.
   - The document is indexed, and a mapping is created for the "price" field.

2. Indexing a Document with a String Representation of a Floating-Point Number:
   - We run a query where the floating-point number is wrapped within double quotes, making it a string value.
   - Elasticsearch successfully indexes the document despite supplying a string value instead of a floating-point number.
   - Type coercion comes into play.
   - Elasticsearch resolves the data type provided for the field, compares it to the mapped data type, and inspects the string value.
   - If the string value contains a numeric value, Elasticsearch converts it to the correct data type.
   - In our example, the string "7.4" is converted to the floating-point number 7.4, and the document is indexed as if a number was initially provided.

3. Indexing a Document with an Invalid String:
   - We run a query where we supply a string that cannot be converted to a float.
   - The query fails because the data type is incorrect, and Elasticsearch is unable to coerce the value into the appropriate data type.

4. Retrieving a Document with a Coerced Value:
   - We retrieve the second document that we indexed.
   - We notice that the value within the "_source" field is a string and not a float.
   - The explanation lies in the fact that the "_source" field contains the original values we indexed, while Elasticsearch internally uses a different data structure (such as the inverted index) to store field values.
   - In our case, within Apache Lucene, the value is stored as a numeric value (float) and not a string.
   - This means that if we make use of the value within the "_source" field, we need to be aware that the value may be either a float or a string, depending on the value supplied at index time.

5. Coercion and Dynamic Mapping:
   - Coercion is not used when determining the data type for a field with dynamic mapping.
   - If a string value is supplied, the data type will be set to "text" even if the string only contains a number.
   - It is recommended to use the correct data types whenever possible, especially when indexing a new field and using dynamic mapping.

6. Disabling Coercion:
   - Whether to disable coercion is a matter of preference.
   - Disabling coercion ensures that Elasticsearch always receives the expected data type and throws an error if the data type is incorrect.
   - Coercion is enabled by default to make Elasticsearch user-friendly and forgiving.
   - To disable coercion, specific configurations can be made, which will be covered later in the course.

In summary, type coercion in Elasticsearch allows for the conversion of field values to the appropriate data type during indexing. Elasticsearch compares the provided data type with the mapped data type and performs conversions when possible. Coercion is enabled by default but can be disabled based on preference. It is essential to be aware of the differences between the "_source" field and the internal data structure used by Elasticsearch when dealing with coerced values.

When working with Elasticsearch, there is no specific "array" data type. Instead, any field can contain zero or more values by default, allowing you to index an array of values without explicitly defining it within the field's mapping.

Here's an overview of arrays in Elasticsearch:

1. Indexing an Array:
   - You can index an array of values without specifying it explicitly in the field's mapping.
   - For example, indexing a "tags" field with an array of values will work out of the box.
   - Elasticsearch maps the "tags" field as a "text" field without indicating that it may contain multiple values.

2. Internal Storage of Arrays:
   - In the case of text fields, the strings in the array are concatenated before analysis.
   - The resulting tokens are stored within an inverted index.
   - Using the Analyze API, you can verify that tokens from all strings in the array are included, with character offsets continuing from the last offset of the previous string.
   - Non-text fields store multiple values within the appropriate data structure in Apache Lucene.

3. Constraint: Same Data Type:
   - All values within an array must be of the same data type.
   - Mixing different data types (e.g., strings and integers) within the same array is not allowed.

4. Coercion of Array Values:
   - Coercion allows for mixing data types in an array as long as the provided types can be coerced into the data type used within the mapping.
   - Coercion is enabled by default.
   - For simple data types, like mixing strings and numbers, coercion works.
   - However, for more complex data types, like mixing booleans and objects, Elasticsearch will return an error because coercion is not possible.

5. Coercion and Mapping Creation:
   - Coercion of array values is only supported when a mapping already exists, either explicitly or through dynamic mapping.
   - When indexing a field for the first time and no mapping exists, dynamic mapping will create a mapping automatically but does not allow mixed data types.
   - It is recommended to provide the correct data type for all array values until the field mapping has been created.

6. Nested Arrays:
   - Elasticsearch supports indexing nested arrays.
   - When indexing a nested array, Elasticsearch flattens it by moving any nested array values to the top level.

7. Arrays of Objects:
   - If you index an array of objects and want to query the objects independently, you need to use the "nested" data type.
   - If querying the objects independently is not required, the "object" data type can be used.

In summary, Elasticsearch supports working with arrays by allowing fields to contain multiple values by default. Arrays can store values of the same data type or mixed data types if coercion is possible. Coercion is enabled by default but should be used with caution. It is important to provide the correct data type for array values until the field mapping is created. Additionally, nested arrays and arrays of objects have specific considerations when it comes to querying and mapping.

1. Define the mappings within a "mappings" key when adding a new index:
```json
PUT /my_index
{
  "mappings": {
    "properties": {
      // Field mappings will be added here
    }
  }
}
```

1. Define field mappings within the "properties" key:
```json
PUT /my_index
{
  "mappings": {
    "properties": {
      "rating": {
        // Mapping for the "rating" field
      },
      "content": {
        // Mapping for the "content" field
      },
      "product_id": {
        // Mapping for the "product_id" field
      },
      "author": {
        // Mapping for the "author" object field
      }
    }
  }
}
```

1. Specify field names as keys and add objects as the values:
```json
PUT /my_index
{
  "mappings": {
    "properties": {
      "rating": {},
      "content": {},
      "product_id": {},
      "author": {}
    }
  }
}
```

1. Specify data types for fields using the "type" key:
```json
PUT /my_index
{
  "mappings": {
    "properties": {
      "rating": {
        "type": "float"
      },
      "content": {
        "type": "text"
      },
      "product_id": {
        "type": "integer"
      },
      "author": {}
    }
  }
}
```

1. Define mappings for the object field ("author"):
```json
PUT /my_index
{
  "mappings": {
    "properties": {
      "rating": {
        "type": "float"
      },
      "content": {
        "type": "text"
      },
      "product_id": {
        "type": "integer"
      },
      "author": {
        "properties": {
          "first_name": {
            "type": "text"
          },
          "last_name": {
            "type": "text"
          },
          "email": {
            "type": "keyword"
          }
        }
      }
    }
  }
}
```

1. Consider the appropriate data type for each field:
   - In this example, "rating" is mapped as a "float" field, "content" as a "text" field, "product_id" as an "integer" field, and "author.email" as a "keyword" field.

2. Run the query to create the index:
   - Execute the query to create the index with the defined mapping:
```json
PUT /my_index
{
  "mappings": {
    "properties": {
      // Field mappings
    }
  }
}
```

1. Index a document into the index:
   - Use a query to index a document into the created index:
```json
POST /my_index/_doc/1
{
  "rating": 4.5,
  "content": "This is a great product.",
  "product_id": 12345,
  "author": {
    "first_name": "John",
    "last_name": "Doe",
    "email": "john.doe@example.com"
  }
}
```

1. Verify the indexing process:
   - Elasticsearch will validate the document's values against the field mappings.
   - If the document contains invalid values, Elasticsearch will refuse to index it.

2.  Naming conventions for field names:
   - There is no strict naming convention, but it's recommended to be consistent in naming fields.
   - Common conventions include camelCase and snake_case for JSON field names.

Remember to adjust the index name, field names, and values to match your specific use case when using these examples.
1. Retrieve the mapping for an entire index:1    - Send a GET request to the Mapping API with the index name:
```json
GET /my_index/_mapping
```
   - This will return the mapping for the specified index, including all field mappings.

2. Retrieve the mapping for a specific field:
   - Use the "field" command followed by the name of the field:
```json
GET /my_index/_mapping/field/my_field
```
   - Replace "my_index" with your index name and "my_field" with the name of the specific field you want to retrieve the mapping for.
   - This will return the mapping for the specified field in the index.

3. Retrieve the mapping for a specific nested field:
   - For objects, use the dot notation to specify the path of the key:
```json
GET /my_index/_mapping/field/author.email
```
   - Replace "my_index" with your index name and "author.email" with the path of the nested field you want to retrieve the mapping for.
   - This will return the mapping for the specified nested field in the index.

4. Analyze the mapping results:
   - The mapping results will show the field names and their corresponding data types, as well as any additional properties defined in the mapping.

By retrieving the mappings, you can verify the mapping settings for an index and ensure that the fields are correctly mapped according to your requirements.

Certainly! Here's the step-by-step process with exemplar code and explanations for mapping objects using dot notation in Elasticsearch:

1. Implicitly map an object using the "properties" mapping parameter:
   - When defining the mapping for an index, use the "properties" key at each level of the hierarchy to implicitly map objects.
   - Here's an example of mapping the "author" field as an object:
```json
PUT /my_index
{
  "mappings": {
    "properties": {
      "author": {
        "properties": {
          "first_name": {
            "type": "text"
          },
          "last_name": {
            "type": "text"
          },
          "email": {
            "type": "keyword"
          }
        }
      }
    }
  }
}
```
   - This mapping defines the "author" field as an object with nested fields "first_name," "last_name," and "email."

2. Map objects using dot notation:
   - Instead of using the "properties" mapping parameter, use a dot notation to define nested fields.
   - Here's an example using dot notation to map the "author" field:
```json
PUT /my_index_v2
{
  "mappings": {
    "author.first_name": {
      "type": "text"
    },
    "author.last_name": {
      "type": "text"
    },
    "author.email": {
      "type": "keyword"
    }
  }
}
```
   - This mapping achieves the same result as the previous approach, but uses dot notation to define the nested fields directly.

3. Retrieve the mapping for the index:
   - Send a GET request to the Mapping API to retrieve the mapping for the index:
```json
GET /my_index_v2/_mapping
```
   - This will return the mapping for the index, which will include the field mappings defined using dot notation.

4. Analyze the mapping results:
   - The mapping results will show the field names and their corresponding data types, whether they were defined using the "properties" mapping parameter or dot notation.

Using dot notation provides a more concise and visually appealing way to define nested field mappings in Elasticsearch. It simplifies the mapping process, especially when dealing with multiple levels of nesting. The dot notation is a convenient shortcut that Elasticsearch translates into the appropriate "properties" mapping behind the scenes.

Note that the dot notation can also be used within search queries to reference specific fields within an object. This makes it a versatile tool for both mapping and querying in Elasticsearch.

Certainly! Here's the step-by-step process with exemplar code and explanations for adding a new field mapping to an existing index in Elasticsearch:

1. Identify the need for a new field mapping:
   - Determine the field that needs to be added to the existing index.
   - For example, let's say we want to add a "created_at" field to the "reviews" index to store the timestamp of when the review was written.

2. Add the new field mapping using the Mapping API:
   - Use the PUT HTTP verb and specify the index name and field mapping in the request body.
   - Since we are adding a field to an existing index, we don't need to include the "mappings" key as we did when creating the index.
   - Instead, specify the "properties" key at the top level of the request body and define the new field mapping within it.
   - Here's an example of adding the "created_at" field mapping:
```json
PUT /reviews/_mapping
{
  "properties": {
    "created_at": {
      "type": "date"
    }
  }
}
```
   - This mapping adds the "created_at" field of type "date" to the existing "reviews" index.

3. Confirm the new field mapping:
   - Retrieve the mapping for the index to ensure that the new field mapping has been added successfully.
   - Send a GET request to the Mapping API:
```json
GET /reviews/_mapping
```
   - The mapping results will include the field mapping for the "created_at" field.

By following these steps, you can easily add a new field mapping to an existing index in Elasticsearch. The Mapping API allows you to modify the structure of your index by defining additional fields. This enables you to adapt your index to accommodate new data requirements or schema changes without recreating the entire index.

Certainly! Here's the step-by-step process with exemplar code and explanations for understanding how dates are handled in Elasticsearch:

1. Understand the different ways to specify dates:
   - Dates can be specified in one of three ways: specially formatted strings, a long number representing milliseconds since the epoch, or an integer representing seconds since the epoch (UNIX timestamp).
   - Elasticsearch expects dates to be in the ISO 8601 format for string timestamps, and UTC is assumed if no timezone is specified.
   - It's important to be familiar with the ISO 8601 format for accurate date representation.

2. Understand how dates are stored in Elasticsearch:
   - Dates are stored as a long number representing the number of milliseconds since the epoch.
   - Even if a string date is supplied, Elasticsearch will parse and convert it to a long number for storage.
   - Dates with timezones are converted to UTC before being stored.
   - All queries, including search queries, are run against this long number representation for consistent date handling.

3. Index documents with different date formats:
   - Prepare queries that index documents with different date formats to observe how Elasticsearch handles them.
   - Include a query with just a date, a query with both date and time, a query with a specified timezone, and a query with a long number representing milliseconds since the epoch.

4. Observe the results and verify the stored values:
   - After indexing the documents, retrieve the indexed documents to observe the values stored in the "created_at" field.
   - Notice that the stored values match the formats specified in the indexing queries.
   - Pay attention to the fact that the stored values represent how the dates are stored internally and are not the same as the original input values.

5. Be cautious with UNIX timestamps:
   - If using a UNIX timestamp, ensure it is specified as milliseconds since the epoch, not seconds.
   - If a UNIX timestamp is specified as seconds, Elasticsearch will treat it as milliseconds, leading to incorrect date representation.
   - Multiply the UNIX timestamp by 1,000 to convert it to milliseconds if needed.

By following these steps, you can gain an understanding of how dates are handled in Elasticsearch, including their storage format and how to specify them in queries. It's important to be familiar with the ISO 8601 format for string timestamps and to be cautious when working with UNIX timestamps to ensure accurate date representation and querying.

Unfortunately, the lecture does not provide explicit code exemplars for updating an existing field mapping. However, I can guide you through the process step by step. Here's how you can update an existing field mapping:

1. Create a new index with the updated mapping: 
   - Define the new mapping with the desired changes, such as changing the data type of the field.
   - Use the PUT mapping API to create the new index with the updated mapping.
   
   ```bash
   PUT new_reviews_index
   {
     "mappings": {
       "properties": {
         "product_id": {
           "type": "keyword"
         },
         // Other existing field mappings
       }
     }
   }
   ```

2. Reindex existing documents into the new index:
   - Use the Reindex API to copy the documents from the old index to the new index, applying the updated mapping.
   
   ```bash
   POST _reindex
   {
     "source": {
       "index": "reviews"
     },
     "dest": {
       "index": "new_reviews_index"
     }
   }
   ```

3. Verify the reindexing process and check the documents in the new index to ensure the mapping changes have taken effect.

4. If everything looks good and you no longer need the old index, you can delete it using the Delete Index API.

   ```bash
   DELETE reviews
   ```

Remember to adjust the index names and field mappings according to your specific case.

Certainly! Here's a breakdown of the steps and code exemplars for updating an existing field mapping using the Reindex API:

1. Create a new index with the updated mapping:
   - Define the new mapping with the desired changes, such as modifying the data type of the field.
   - Use the PUT mapping API to create the new index with the updated mapping.
   
   ```bash
   PUT new_reviews_index
   {
     "mappings": {
       "properties": {
         "product_id": {
           "type": "keyword"
         },
         // Other existing field mappings
       }
     }
   }
   ```

2. Reindex existing documents into the new index:
   - Use the Reindex API to copy the documents from the old index to the new index, applying the updated mapping.
   - Specify the source index and destination index in the request body.
   - Optionally, you can provide a query to reindex only a subset of documents that match the query.
   - You can also use a script to modify documents during reindexing.
   
   ```bash
   POST _reindex
   {
     "source": {
       "index": "reviews"
     },
     "dest": {
       "index": "new_reviews_index"
     },
     "script": {
       "source": "if (ctx._source.product_id != null) { ctx._source.product_id = ctx._source.product_id.toString() }"
     }
   }
   ```

3. Verify the reindexing process and check the documents in the new index to ensure the mapping changes have taken effect.

4. If everything looks good and you no longer need the old index, you can delete it using the Delete Index API.

   ```bash
   DELETE reviews
   ```

Please note that the script provided in the example converts the `product_id` field to a string type during reindexing. Adjust the script according to your specific needs.

Remember to adjust the index names, field mappings, and script according to your specific case.

## Updating Field Mapping with Reindex API

1. Create a new index with the updated mapping:
   - Define the new mapping with the desired changes, such as modifying the data type of the field.
   - Use the PUT mapping API to create the new index with the updated mapping.
   
   ```bash
   PUT new_reviews_index
   {
     "mappings": {
       "properties": {
         "product_id": {
           "type": "keyword"
         },
         // Other existing field mappings
       }
     }
   }
   ```

2. Reindex existing documents into the new index:
   - Use the Reindex API to copy the documents from the old index to the new index, applying the updated mapping.
   - Specify the source index and destination index in the request body.
   - Optionally, you can provide a query to reindex only a subset of documents that match the query.
   - You can also use a script to modify documents during reindexing.
   
   ```bash
   POST _reindex
   {
     "source": {
       "index": "reviews"
     },
     "dest": {
       "index": "new_reviews_index"
     },
     "script": {
       "source": "if (ctx._source.product_id != null) { ctx._source.product_id = ctx._source.product_id.toString() }"
     }
   }
   ```

3. Verify the reindexing process and check the documents in the new index to ensure the mapping changes have taken effect.

4. If everything looks good and you no longer need the old index, you can delete it using the Delete Index API.

   ```bash
   DELETE reviews
   ```

### Source Filtering

To reduce the disk space used by fields you don't need in the new index, you can use source filtering. It allows you to include only specified fields in the `_source` object for each document during reindexing.

Here's an example of using source filtering to exclude the "field1" and "field2" from the reindexed documents:

```bash
POST _reindex
{
  "source": {
    "index": "source_index",
    "_source": ["field3", "field4"]
  },
  "dest": {
    "index": "destination_index"
  }
}
```

In this example, only "field3" and "field4" will be included in the documents when they are reindexed into the destination index. Any other fields will be excluded.

### Renaming a Field

You can rename a field during the reindexing process using a script. Here's an example that renames the "content" field to "comment":

```bash
POST _reindex
{
  "source": {
    "index": "source_index"
  },
  "dest": {
    "index": "destination_index"
  },
  "script": {
    "source": "ctx._source.comment = ctx._source.remove('content')"
  }
}
```

In this example, the script removes the "content" field and assigns its value to the newly created "comment" field in the reindexed documents.

### Advanced Use Cases

1. Specify a query within the "source" parameter:
   - Reindex only documents that match a specific query.
   - Useful when you want to reindex a subset of documents from the source index.
   
   ```bash
   POST _reindex
   {
     "source": {
       "index": "source_index",
       "query": {
         "range": {
           "rating": {
             "gte": 4.0
           }
         }
       }
     },
     "dest": {
       "index": "destination_index"
     }
   }
   ```

2. Deleting documents during reindexing:
   - Use the "delete" operation within a script to remove documents from the destination index.
   - Specify a condition within the script to determine which documents to delete.
   
   ```bash
   POST _reindex
   {
     "source": {
       "index": "source_index"
     },
     "dest": {
       "index": "destination_index"
     },
     "script": {
       "source": "if (ctx._source.rating < 4.0) { ctx.op = 'delete' }"
     }
   }
   ```

These are just a few examples of how you can use the Reindex API for different scenarios. Remember to adjust the index names, field mappings, queries, and scripts according to your specific requirements.

For more details and advanced features of the Reindex API, refer to the Elasticsearch documentation.

## Using Field Aliases

In the previous lecture, we discussed how to rename a field by reindexing documents into a new index. However, if you have millions of documents, reindexing just for the sake of renaming a field may not be practical. In such cases, you can use field aliases as an alternative solution.

1. Implementing field aliases:
   - Instead of renaming the field, add an alias that points to the actual field.
   - Add a new field mapping of type "alias" and specify the target field name using the "path" parameter.
   
   ```bash
   PUT reviews/_mapping
   {
     "properties": {
       "comment": {
         "type": "alias",
         "path": "content"
       }
     }
   }
   ```

2. Search using the original field or the alias:
   - Prepare search queries that use the original field name and the alias, respectively.
   - Querying the alias will provide the same results as querying the original field.
   
   ```bash
   GET reviews/_search
   {
     "query": {
       "match": {
         "content": "search keyword"
       }
     }
   }
   ```

   ```bash
   GET reviews/_search
   {
     "query": {
       "match": {
         "comment": "search keyword"
       }
     }
   }
   ```

3. Verify that both queries return the same results.

Using a field alias allows you to query a field by a different name without the need to reindex the data. It does not replace the existing field mapping but provides an additional way to reference the field in queries.

Field aliases can be updated to point to a different target field by performing a mapping update with a new value for the "path" parameter. This flexibility is possible because aliases have no impact on how values are indexed; they are used solely for query parsing in search or index requests.

Field aliases have a few limitations, but for common use cases, they can be utilized as expected. Additionally, it is possible to configure index aliases at the cluster level, which is useful when dealing with high volumes of data. However, further details on cluster-level index aliases are beyond the scope of this section.

Field aliases provide a convenient way to rename fields without the need for reindexing and offer flexibility in query parsing. They can be a valuable tool in scenarios where renaming fields is required while maintaining backward compatibility.

For more information and advanced use cases related to field aliases, refer to the Elasticsearch documentation.

## Multiple Mappings for a Field

It may surprise you, but a field in Elasticsearch can have multiple mappings, allowing it to be mapped in different ways simultaneously. In this lecture, we'll explore an example where a "text" field is also mapped as a "keyword" field.

1. Creating a throwaway index with two fields:
   - Prepare a simple query that creates an index with two fields: "description" and "ingredients".
   - By default, every field in Elasticsearch can store zero or more values.
   
   ```bash
   PUT recipes
   {
     "mappings": {
       "properties": {
         "description": {
           "type": "text"
         },
         "ingredients": {
           "type": "text"
         }
       }
     }
   }
   ```

2. Indexing a document:
   - Index a document into the created index using a prepared query.
   - When indexing, there is no sign of the "keyword" mapping; the field is specified as if no additional mapping exists.
   
   ```bash
   POST recipes/_doc/1
   {
     "description": "Delicious spaghetti recipe",
     "ingredients": ["pasta", "tomato sauce", "meatballs"]
   }
   ```

3. Behind the scenes of indexing:
   - "Text" fields are analyzed, and an inverted index is created with terms emitted by the analyzer.
   - In addition to the "text" mapping, an inverted index is created for the "ingredients" field using the "keyword" analyzer.
   - The "keyword" inverted index contains unmodified values optimized for exact matches, aggregations, and sorting.
   
4. Querying the field mappings:
   - Perform a "match_all" search query to see that the "ingredients" field within the results looks normal.
   - To query the "keyword" mapping for exact matches, use a "term" query and specify the field name with the "keyword" mapping.
   
   ```bash
   GET recipes/_search
   {
     "query": {
       "match_all": {}
     }
   }
   ```

   ```bash
   GET recipes/_search
   {
     "query": {
       "term": {
         "ingredients.keyword": "pasta"
       }
     }
   }
   ```

   - The "term" query targets the inverted index containing the raw string values, bypassing analysis.

5. Utilizing multiple mappings for a field:
   - Multiple mappings for a field allow you to query it in different ways.
   - In the example, the "text" mapping is used for full-text searches, while the "keyword" mapping is used for aggregations and sorting.
   - Multi-fields offer more control over how values are indexed beyond just the data type, such as configuring synonyms or stemming for a single field.

Multiple mappings for a field are powerful and enable versatile querying and indexing capabilities. They are commonly used to handle different requirements for full-text searches, aggregations, and sorting within the same field.

Feel free to delete the temporary index when it's no longer needed.

In the next lecture, we will explore more advanced concepts. Stay tuned!

## Index Templates

In this lecture, we will explore index templates, which define settings and/or mappings for indices that match specific patterns. Index templates are only applied to new indices and are useful for automating the configuration of index mappings and settings.

1. Adding an index template:
   - Use the Index Template API with the PUT HTTP verb to add a new index template.
   - Specify the index template name, such as "access-logs", which defines mappings for indices storing HTTP access logs.
   - The "index_patterns" parameter is used to define the index patterns that the template should be applied to. Use wildcard expressions to match multiple indices.
   - Optionally, define mappings and settings within the template.
   
   ```bash
   PUT _template/access-logs
   {
     "index_patterns": ["access-*"],
     "mappings": {
       "properties": {
         "field1": {
           "type": "text"
         },
         "field2": {
           "type": "keyword"
         }
       }
     },
     "settings": {
       "number_of_shards": 5,
       "number_of_replicas": 1
     }
   }
   ```

2. Creating an index that matches the index template:
   - Create a new index, such as "access-logs-2020-01-01", that matches the index pattern defined in the template.
   - Inspect the index using the GET HTTP verb to ensure that the mappings and settings were applied as expected.
   
   ```bash
   PUT access-logs-2020-01-01
   ```

   ```bash
   GET access-logs-2020-01-01
   ```

   - The mapping and settings defined in the index template are present in the index.

3. Merging settings and mappings:
   - If a new index creation request specifies additional settings or mappings, they will be merged with the index template configuration.
   - In case of duplicate entries, the values specified in the new index request take precedence over the index template.
   
4. Handling multiple index templates:
   - An index may match multiple index templates.
   - Index templates can have an "order" parameter to control the priority of template settings when there are multiple matches.
   - The configuration from the template with the highest order takes precedence.
   
5. Updating index templates:
   - Index templates can be updated by using the same API as when creating the template.
   - Send the full new configuration to update mappings or settings.
   - Existing indices that matched the index template are not modified.
   
6. Retrieving and deleting index templates:
   - Use the GET and DELETE HTTP verbs with the same endpoint to retrieve or delete an index template.
   
7. Elastic Common Schema (ECS):
   - The field names used in the example may seem lengthy due to the Elastic Common Schema (ECS), which will be covered in the next lecture.
   - ECS provides a standardized and consistent naming convention for fields in log data.
   
Index templates are powerful for automating the configuration of mappings and settings for new indices that match specific patterns. They allow for consistency and efficiency when working with multiple indices.

In the next lecture, we'll explore the Elastic Common Schema (ECS) in more detail.

Certainly! Here's the updated version of the notes with explanations about the Elastic Common Schema (ECS):

## Elastic Common Schema (ECS)

In the previous lecture, we discussed the Elastic Common Schema (ECS), which is a specification that defines a set of common fields and their mappings in Elasticsearch. ECS was introduced to establish a standard naming convention and ensure cohesion between mappings when ingesting data from different sources into Elasticsearch.

1. Motivation for ECS:
   - In the past, field names varied depending on the source, leading to confusion and inconvenience.
   - For example, different web servers used different field names for the same data, making it difficult for data consumers like Kibana to work with the data.
   - ECS aims to provide consistent field names regardless of the data source, enabling easier consumption and analysis of data.

2. @timestamp Field:
   - ECS defines common fields, such as the "@timestamp" field, which represents the timestamp when an event originated.
   - Regardless of the event source, the field is named "@timestamp" in ECS, simplifying data consumption and eliminating the need to know the event source implementation.
   - Note that the @timestamp field is used for events, while other entities like products may have their own timestamp fields (e.g., "created_at").

3. Field Sets in ECS:
   - ECS defines multiple field sets that cover various categories, including network fields, geolocation fields, operating system fields, and more.
   - These field sets consist of hundreds of fields that cater to different types of events.
   - The ECS Field Reference in the documentation provides an overview of the available field sets.

4. Events and Use Cases:
   - In ECS, documents are referred to as events, as ECS aims to support a wide range of event types generated by various technologies.
   - ECS is not limited to web server logs but covers diverse use cases such as operating system metrics, geospatial data, and more.
   - It is most useful when storing standard events where the field structure aligns with ECS, enabling the utilization of preconfigured Kibana dashboards without field name reconfiguration.

5. Automatic ECS Mapping:
   - Tools like Filebeat and Metricbeat often structure data according to ECS automatically.
   - When using Filebeat to ingest web server logs, ECS is handled for you, eliminating the need for manual ECS configuration.
   - ECS becomes more relevant when building custom implementations that don't involve other Elastic Stack products.

6. Awareness of ECS:
   - While you may not actively work with ECS in most use cases, it's beneficial to be aware of its existence and understand its role in maintaining consistency across the Elastic Stack.
   - Consider ECS a best practice and recommendation when structuring data, but it's not mandatory for every scenario.
   - If you're interested, the documentation provides further details on ECS and the fields it offers.

ECS simplifies data ingestion and analysis by providing a standardized field naming convention for common events. While its primary impact is felt when working with standard events, understanding ECS is valuable for maintaining consistency in your data structures.

Certainly! Here's the updated version of the notes with explanations about dynamic mapping:

## Dynamic Mapping

In this section, we will explore dynamic mapping, which allows Elasticsearch to automatically create field mappings without the need for explicit mappings. Dynamic mapping makes Elasticsearch easier to use by eliminating the requirement of defining mappings before indexing documents.

1. Automatic Field Mapping:
   - When indexing a document into a new or unmapped index, Elasticsearch automatically creates field mappings for each encountered field.
   - Let's examine the field mappings that would be generated for a document with three fields.

2. Field Mapping Examples:
   - The "created_at" field is mapped as the "date" data type, despite being specified as a string. Elasticsearch uses date detection to identify and parse dates from string values.
   - The "in_stock" field is mapped as the "long" data type since it contains a numeric value without decimals. Elasticsearch chooses the "long" data type by default, but explicitly mapping it as an integer could save disk space.
   - The "tags" field is interestingly mapped as a multi-field with both the "text" and "keyword" data types. The "keyword" mapping follows the naming convention discussed earlier.
   - Elasticsearch adds multiple mappings to provide flexibility for different use cases. The "text" mapping is suitable for full-text searches, while the "keyword" mapping is optimized for exact matches, aggregations, and sorting.

3. Sensible Default Behavior:
   - Elasticsearch's default behavior aims to cover various use cases but might not always provide the most optimal mappings.
   - For example, using the "text" mapping for the "tags" field might be unnecessary if it will only be used for exact matches and aggregations.
   - The "ignore_above" parameter with a value of 256 is used to ignore long strings in the "keyword" mapping. This prevents storing excessively long values that are unlikely to be used for sorting or aggregations.

4. Optimization Considerations:
   - While Elasticsearch's default dynamic mapping is convenient, it may lead to unnecessary disk space usage and indexing overhead.
   - For small-scale deployments, the impact is negligible. However, with millions of documents, it's beneficial to optimize mappings.
   - Explicitly mapping fields or disabling mappings that won't be used can save disk space and improve indexing performance.
   - Consider the scale of your index and evaluate whether custom mappings are necessary for efficiency gains.

5. Dynamic Mapping Rules:
   - Elasticsearch follows specific rules to determine how fields are dynamically mapped:
     - Strings are typically mapped to a "text" field with a nested "keyword" mapping, except for cases where the value matches a date format or numeric value.
     - Numeric detection allows mapping strings containing only numbers to either "float" or "long" fields.
     - Integers are mapped to the "long" data type, as Elasticsearch cannot infer the intended range.
     - Floating-point numbers and booleans are mapped to "float" and "boolean" fields, respectively.
     - Objects are mapped as objects, and the key-value pairs within the object follow the same mapping rules.
     - Arrays are mapped similarly to other fields, with the data type inferred from the first non-null value within the array.
     - NULL values are ignored, and Elasticsearch does not create mappings for such fields.

6. Dynamic Mapping in Practice:
   - When indexing documents into the "products" index without explicit mappings, Elasticsearch automatically generated field mappings based on the field values supplied via the Bulk API.
   - The mapping for the "description" and "tags" fields includes both "text" and "keyword" mappings, which may not always be the most efficient configuration.

Dynamic mapping allows Elasticsearch to adapt to varying field structures, making it more user-friendly. However, it's important to consider the specific requirements and scale of your deployment to optimize mappings for efficiency.

## Choosing between Explicit and Dynamic Mapping

Now that we have explored both explicit and dynamic mapping, you might wonder which approach to choose. However, it's important to note that you don't necessarily have to choose one or the other. In fact, these two approaches can complement each other effectively. Let's dive into an example to illustrate this concept.

1. Example Scenario:
   - We will work with a simple example to demonstrate the combination of explicit and dynamic mapping.
   - First, we will create a new index named "people" with an explicit mapping for the "first_name" field using the "text" data type.
   - The mapping query is executed in advance, and you can see the resulting mapping to the right.

```bash
PUT /people
{
  "mappings": {
    "properties": {
      "first_name": {
        "type": "text"
      }
    }
  }
}
```

2. Dynamic Mapping Example:
   - Next, let's index a document that includes both a first and last name into the "people" index.
   - Since there is no explicit mapping for the "last_name" field, we can observe what happens when dynamic mapping comes into play.

```bash
POST /people/_doc
{
  "first_name": "John",
  "last_name": "Doe"
}
```

3. Retrieving the Mapping:
   - After indexing the document, let's retrieve the mapping for the "people" index again to see if the "last_name" field has been mapped.

```bash
GET /people/_mapping
```

4. Result:
   - The response will show that the "last_name" field has been automatically mapped.
   - This behavior occurs because dynamic mapping is enabled by default and the field did not have a pre-existing mapping.
   - Elasticsearch automatically creates a field mapping for the new field, following the same rules as shown in the previous lecture.

The example demonstrates how explicit and dynamic mapping can be combined. In this case, we had an explicit mapping for the "first_name" field but not for the "last_name" field. Dynamic mapping kicks in when a field without a pre-defined mapping is encountered, allowing Elasticsearch to automatically create a field mapping.

This combination of explicit and dynamic mapping provides flexibility. You can define mappings for fields that you know in advance and allow dynamic mapping to handle new fields that arise during indexing. By leveraging both approaches, you can ensure that your index is well-structured while accommodating unforeseen fields.

Remember, these recommendations are based on your specific use case and the level of control you desire over the index mappings.

## Configuring Dynamic Mapping

Now that you understand how dynamic mapping maps values to field mappings by default, let's explore how it can be configured to fit your needs.

1. Disabling Dynamic Mapping:
   - To disable dynamic mapping and prevent Elasticsearch from automatically creating mappings for new fields, you can set the "dynamic" setting to "false" within the "mappings" key.
   - Let's disable dynamic mapping by setting the "dynamic" value to "false" and add the index again.

```bash
PUT /people
{
  "mappings": {
    "dynamic": false,
    "properties": {
      "first_name": {
        "type": "text"
      }
    }
  }
}
```

2. Indexing a Document with New Field:
   - Let's index a document containing an additional field, "last_name," which is not defined in the mapping.

```bash
POST /people/_doc
{
  "first_name": "John",
  "last_name": "Doe"
}
```

3. Retrieving the Mapping:
   - Upon retrieving the mapping, you will notice that the "last_name" field is not mapped.
   - However, the document was indexed successfully and contains both fields when viewed in the "_source" object.

```bash
GET /people/_mapping
```

4. Explanation:
   - Disabling dynamic mapping with the "dynamic" setting set to "false" instructs Elasticsearch to ignore new fields.
   - While the field is still part of the "_source" object, it is not indexed or searchable because it lacks a field mapping.
   - Leaving out fields during indexing is valid but renders the field non-indexed and unusable in queries.

5. Using "strict" Dynamic Mapping:
   - Another option for the "dynamic" setting is to set it as "strict."
   - With "strict" dynamic mapping, Elasticsearch rejects any document that contains an unmapped field, similar to a relational database schema.

```bash
DELETE /people

PUT /people
{
  "mappings": {
    "dynamic": "strict",
    "properties": {
      "first_name": {
        "type": "text"
      }
    }
  }
}
```

6. Indexing with Strict Dynamic Mapping:
   - Running the index query again will result in an error because the "last_name" field is not allowed due to the "dynamic" setting being set to "strict."

```bash
POST /people/_doc
{
  "first_name": "John",
  "last_name": "Doe"
}
```

7. Fine-Grained Dynamic Mapping:
   - Dynamic mapping can be inherited to provide fine-grained control over specific fields.
   - In this example, we want to strictly control the mapping for the "specifications" field while allowing dynamic mapping for the "other" field.

```bash
PUT /computers
{
  "mappings": {
    "dynamic": "strict",
    "properties": {
      "name": {
        "type": "keyword"
      },
      "specifications": {
        "dynamic": "strict",
        "properties": {
          "cpu": {
            "properties": {
              "name": {
                "type": "text"
              }
            }
          }
        }
      },
      "other": {
        "dynamic": true
      }
    }
  }
}
```

8. Adding New Fields Dynamically:
   - In the "other" field, which is an object, we can add new fields dynamically without predefining them in the mapping.

```bash
POST /computers/_doc
{
  "name": "Desktop",
  "specifications": {
    "cpu": {
      "name": "Intel Core i7",
      "frequency": "3.6 GHz"
    }
  },
  "other": {
    "security": "Fingerprint Scanner"
  }
}
```

9. Numeric Detection:
   - Numeric detection allows Elasticsearch to detect if a string contains only numeric values and automatically assigns the "float" or "long" data type during dynamic mapping.
   - Enable numeric detection by setting the "numeric_detection" setting to "true" at the root level of the "mappings" object.

10. Date Detection:
    - Elasticsearch inspects string values to detect dates based on the default date formats.
    - If a match is found and dynamic mapping is enabled, Elasticsearch creates a "date" field for the detected date value.
    - You can disable date detection by setting the "date_detection" setting to "false."
    - Additionally, you can configure custom dynamic date formats to recognize non-standard date formats sent to Elasticsearch.

These are some of the common ways to configure dynamic mapping. Understanding these options allows you to customize Elasticsearch's behavior according to your specific requirements.

Certainly! Here are the revised notes with explanations, including code snippets, intended for a reader who is not familiar with HTTP commands, JSON files, parameters, or Elasticsearch:

## Dynamic Templates for Dynamic Mapping

Dynamic templates offer a way to configure dynamic mapping in Elasticsearch. They consist of conditions and field mappings to be used when a new field is encountered without any existing mapping.

1. Dynamic templates are added within the "dynamic_templates" key, which is nested within the "mappings" key.

```json
PUT /my_index
{
  "mappings": {
    "dynamic_templates": [
      {
        "integers": {
          "match_mapping_type": "long",
          "mapping": {
            "type": "integer"
          }
        }
      }
    ]
  }
}
```

2. In this example, we define a dynamic template named "integers" that applies to whole number fields.
   - The "match_mapping_type" parameter specifies the JSON data type to match.
   - We set the match type to "long" to match whole number fields.
   - The field mapping in the "mapping" parameter sets the data type to "integer."

3. Let's index a document with a field that matches the condition defined in the dynamic template.

```json
POST /my_index/_doc
{
  "my_field": 42
}
```

4. By default, this new field would be mapped as a "long" field, but the dynamic template should change it to an "integer" field.

5. Let's retrieve the mapping to verify the field mapping.

```json
GET /my_index/_mapping
```

6. In the retrieved mapping, you will see that the field has been mapped as an "integer" instead of a "long" as per the dynamic template.

7. Dynamic templates allow you to customize field mappings based on conditions, providing flexibility for mapping new fields.

8. Another example is adjusting how strings are mapped. By default, strings are mapped as both "text" and "keyword" fields. However, you may want to change this behavior.

```json
PUT /my_index
{
  "mappings": {
    "dynamic_templates": [
      {
        "strings": {
          "match_mapping_type": "string",
          "mapping": {
            "type": "text",
            "ignore_above": 512
          }
        }
      }
    ]
  }
}
```

9. In this example, the dynamic template "strings" applies to string fields and maps them as "text" fields.
   - The "ignore_above" parameter defines the maximum length of the string to be indexed.

10. Dynamic templates can be used to tweak the default mapping rules to fit your needs.

11. Advanced dynamic templates offer more options beyond matching the JSON data type.

12. The "match" and "unmatch" parameters allow you to specify conditions based on the field name.

```json
PUT /my_index
{
  "mappings": {
    "dynamic_templates": [
      {
        "text_fields": {
          "match": "text_*",
          "unmatch": "*_keyword",
          "mapping": {
            "type": "text"
          }
        }
      },
      {
        "keyword_fields": {
          "match": "*_keyword",
          "mapping": {
            "type": "keyword"
          }
        }
      }
    ]
  }
}
```

13. In this example, the "text_fields" template matches fields starting with "text_" but excludes those ending with "_keyword".
   - The "keyword_fields" template matches fields ending with "_keyword".
   - Fields matching the patterns defined in the dynamic templates will be mapped as "text" or "keyword" fields accordingly.

14. You can use wildcards (*) in the "match" and "unmatch" parameters to provide flexibility.

15. For even more flexibility, the "match_pattern" parameter can be set to "regex" to support regular expressions in the "match" parameter.

16. Here's an example using the "match_pattern" parameter with regular expressions:

```json
PUT /my_index
{
  "mappings": {
    "dynamic_templates": [
      {
        "regex_fields": {
          "match_pattern": "regex",
          "match": ".*_name$",
          "mapping": {
            "type": "text"
          }
        }
      }
    ]
  }
}
```

17. In this example, the dynamic template "regex_fields" uses a regular expression to match fields ending with "_name".
   - Fields matching this pattern will be mapped as "text" fields.

18. The "path_match" and "path_unmatch" parameters match the full field path, including nested fields.

```json
PUT /my_index
{
  "mappings": {
    "dynamic_templates": [
      {
        "nested_fields": {
          "path_match": "name.*",
          "mapping": {
            "type": "text"
          }
        }
      }
    ]
  }
}
```

19. In this example, the dynamic template "nested_fields" matches fields under the "name" object.
   - The wildcard (*) in the "path_match" parameter matches all keys under the "name" object.
   - Fields matching this pattern will be mapped as "text" fields.

20. You can also use wildcards in the field path.

21. Dynamic templates support placeholders within string values. One such placeholder is "dynamic_type," which represents the detected data type.

```json
PUT /my_index
{
  "mappings": {
    "dynamic_templates": [
      {
        "dynamic_type_template": {
          "match_mapping_type": "*",
          "mapping": {
            "type": "{dynamic_type}",
            "index": false
          }
        }
      }
    ]
  }
}
```

22. In this example, the dynamic template "dynamic_type_template" matches all data types.
   - The "{dynamic_type}" placeholder is used to set the field mapping data type dynamically.
   - The "index" parameter is set to "false" to disable indexing for all fields matched by this template.

23. This example shows how placeholders can be used to add flexibility and reduce the need for multiple dynamic templates.

24. Dynamic templates are helpful for optimizing mappings based on specific conditions, such as time series data.

25. Before concluding, let's briefly differentiate between dynamic templates and index templates:
   - An index template applies fixed field mappings and index settings when its pattern matches an index's name.
   - A dynamic template, on the other hand, dynamically adds mappings for fields that match specified conditions when dynamic mapping is enabled.

These explanations and code examples should help you understand dynamic templates and their usage in Elasticsearch, even if you're not familiar with HTTP commands, JSON files, parameters, or Elasticsearch itself.

Sure! Here are the revised notes with explanations, including code snippets, intended for a reader who is not familiar with HTTP commands, JSON files, parameters, or Elasticsearch:

## Mapping Recommendations

Before we dive back into analyzers, I'd like to share a couple of recommendations regarding mapping in Elasticsearch. These are my personal opinions, so feel free to decide whether or not to follow them.

1. **Use explicit mapping, especially for production clusters:** Dynamic mapping is convenient during development, but the generated field mappings may not be the most efficient. Explicit mappings can optimize disk space usage and improve performance, especially when storing a high number of documents.

```json
PUT /my_index
{
  "mappings": {
    "dynamic": "strict",
    // other mappings...
  }
}
```

2. To use explicit mappings, set the "dynamic" parameter to "strict" instead of "false". Setting it to "false" allows adding unmapped fields, but they will be ignored during indexing. However, querying these fields won't produce any results, leading to unexpected search outcomes. Using strict mapping ensures better control over the index.

3. **Avoid mapping "text" fields as both "text" and "keyword" by default:** Dynamic mapping maps text fields as both "text" and "keyword" fields, which consumes additional disk space. Instead, consider your querying requirements and map the field accordingly:
   - For full-text searches, add a "text" mapping.
   - For aggregations, sorting, or filtering based on exact values, add a "keyword" mapping.
   - Mapping a field in both ways is typically unnecessary unless you have specific use cases.

4. If you have control over the application sending data to Elasticsearch, **disable type coercion**. Type coercion allows Elasticsearch to handle incorrect data types, but it's better to provide the correct data types in the JSON objects.

5. For numeric fields, consider the appropriate data type based on your indexing needs. Sometimes mapping a field as "long" is unnecessary, and an "integer" would be sufficient. "Long" can store larger numbers but requires more disk space. Similarly, "double" requires twice as much disk space as "float". Choose the data type that suits your precision and space requirements.

6. **Utilize mapping parameters to limit stored data**: Elasticsearch (based on Apache Lucene) provides several mapping parameters to control the amount of stored data:
   - If a field won't be used for sorting, aggregations, and scripting, set "doc_values" to "false" to save disk space.
   - If a field won't be used for relevance scoring, set "norms" to "false" to avoid storing relevance scoring-related data.
   - If a field won't be used for filtering, disable indexing by setting "index" to "false". The field can still be used for aggregations, making it suitable for time series data.

7. These parameters are beneficial when dealing with a large number of documents, resulting in significant space savings. However, for a small number of documents, the effort required to handle these parameters may outweigh the limited savings.

8. There's no specific rule for when to use these parameters. As a general guideline, it's typically worth considering for datasets with a million or more documents.

9. If you anticipate storing millions of documents, optimize your mappings from the beginning to avoid reindexing later. However, if you didn't optimize initially, it's not a significant issue as you can always reindex documents into a new index.

10. These recommendations provide a good starting point for mapping optimization. Depending on your specific use case, there may be additional optimizations available. However, these suggestions cover the most common scenarios.

Feel free to adjust these recommendations based on your needs and requirements. Mapping plays a crucial role in Elasticsearch performance, and considering these suggestions can help you optimize your index efficiently.

## Stemming and Stop Words

Let's now discuss two important concepts related to text analysis in Elasticsearch: stemming and stop words.

1. **Stemming:** Stemming is the process of reducing words to their root form. It helps address the issue of different word forms (e.g., tense, plural, possessive) by mapping them to a common base form. For example, the word "loved" can be stemmed to "love," and "drinking" can be stemmed to "drink." Elasticsearch uses stemming internally to improve search results. However, not all stemmed words are valid dictionary words, depending on the configured stemming aggressiveness.

2. **Stop Words:** Stop words are commonly occurring words that provide little to no value in terms of relevance. They are often filtered out during the text analysis process. Examples of stop words include "a," "the," "at," "of," and "on." These words are unlikely to affect the relevance of search results and are typically removed to improve performance. However, Elasticsearch's relevance algorithm has become better at limiting the influence of stop words on search results, so it is not necessary to remove them in most cases.

```json
GET /my_index/_analyze
{
  "analyzer": "standard",
  "text": "This is an example of text analysis."
}
```

3. By default, Elasticsearch's "standard" analyzer does not remove stop words. However, you can use custom analyzers or specific language analyzers that may include stop word removal as part of the analysis process.

4. Removing stop words used to be more popular in the past, but it is now less common due to the improved relevance algorithms. The default behavior of Elasticsearch's "standard" analyzer is to retain stop words.

5. Understanding stemming and stop words, let's now explore how analyzers are used during document searches.

```json
GET /my_index/_search
{
  "query": {
    "match": {
      "content": "searching documents"
    }
  }
}
```

6. When searching for documents, the search query is analyzed using the same analyzer configured for the target field. This ensures that the query terms are processed consistently with the indexed documents.

7. The analysis process includes steps such as lowercasing, tokenization (splitting text into individual tokens), stemming, and stop word removal (if applicable). The processed query terms are then matched against the indexed tokens for retrieval.

Understanding how stemming, stop words, and analyzers work together helps improve search accuracy and relevance. Analyzers play a crucial role in ensuring consistent analysis of both indexed documents and search queries.

## Analyzers in Search Queries

In the previous lecture, I explained how analyzers are used when indexing "text" fields. Now, let's discuss how analyzers come into play during search queries.

1. When indexing a document, the field values are processed by the configured analyzer for the field. The analysis process includes steps such as lowercasing, tokenization, stemming, and stop word removal. The analyzed terms are then stored in the inverted index for efficient searching.

2. However, you might wonder how we can search for values that have undergone analysis and potentially changed. Let's clarify this with an example.

```json
GET /my_index/_analyze
{
  "analyzer": "stemming_analyzer",
  "text": "I love drinking bottles of wine."
}
```

3. In this example, we use a custom analyzer named "stemming_analyzer" that behaves similarly to the "standard" analyzer but also performs stemming for English words. The diagram shows how the sentence is analyzed, with terms lowercased, some words stemmed, and punctuation removed.

4. Now, suppose we search for the term "drinking." During indexing, the word "drinking" was stemmed to its root form, which is "drink." So, will the document match the query?

5. Yes, it will. The search query goes through the same analysis process as when the field value was indexed. Elasticsearch examines the mapping for the "description" field, determines that it's a "text" field, and checks for the configured analyzer.

6. In this example, the "stemming_analyzer" is specified in the field mapping, so it is used during the search. The search query term "drinking" is also stemmed by the analyzer, resulting in the term "drink." This matches the term stored within the inverted index for the "description" field, and thus, the document is considered a match.

7. It's important to note that the same analyzer is used both during indexing and at search time to ensure consistent analysis. This consistency prevents unpredictable search results.

8. By default, queries on "text" fields are case-insensitive. For example, if a query is entered in all capitalized letters, it will be lowercased at search time by the "standard" analyzer. However, case sensitivity can be altered by specifying a different analyzer, although this is rarely necessary and requires caution.

Understanding that analyzers are used consistently during indexing and search queries helps ensure accurate matching of values, even if they differ from the original field values specified in the search query.

## Built-in Analyzers and Custom Analyzers

In Elasticsearch, there are several built-in analyzers available for your convenience. These analyzers are pre-configured combinations of character filters, token filters, and a tokenizer. Let's explore the most important ones:

1. The "standard" analyzer is the default analyzer we've discussed previously. It splits text into terms at word boundaries, removes punctuation, and lowercases letters. It also includes an optional "stop" token filter to remove common stop words (disabled by default).

2. The "simple" analyzer is similar to the "standard" analyzer but splits the input text by anything other than a letter. It lowercases terms using the "lowercase" tokenizer, which is a performance hack to avoid redundant processing.

3. The "whitespace" analyzer splits the input text at whitespace without lowercasing letters. It preserves the original case of terms.

4. The "keyword" analyzer is a no-op analyzer that leaves the input text intact and outputs it as a single term. This analyzer is used for fields of the "keyword" data type, where exact matching is required.

5. The "pattern" analyzer allows you to define a regular expression to match token separators, determining how the input text is split into tokens. It offers flexibility in defining custom splitting patterns.

Additionally, Elasticsearch provides language-specific analyzers. These analyzers handle language-specific quirks and are good starting points for most use cases. You can find the list of available language analyzers in the Elasticsearch documentation.

To use these analyzers within field mappings, simply specify the name of the analyzer in the "analyzer" mapping parameter. For example, to use the "english" analyzer for a "description" field:

```json
{
  "mappings": {
    "properties": {
      "description": {
        "type": "text",
        "analyzer": "english"
      }
    }
  }
}
```

While the built-in analyzers can be used as-is, many of them can also be customized by adjusting their behavior. For example, the "standard" analyzer can be configured to remove stop words, which is not enabled by default. To configure a built-in analyzer, you can create a custom analyzer by extending the existing analyzer.

Here's an example of creating a custom analyzer named "remove_english_stop_words" by extending the "standard" analyzer:

```json
{
  "settings": {
    "analysis": {
      "analyzer": {
        "remove_english_stop_words": {
          "type": "standard",
          "stopwords": "_english_"
        }
      }
    }
  }
}
```

In this example, the custom analyzer removes English stop words by specifying the "stopwords" parameter with the value "_english_". The structure of the query might appear different, but we will cover it in detail in the next lecture.

To use the custom analyzer, simply specify its name in the field mapping:

```json
{
  "mappings": {
    "properties": {
      "description": {
        "type": "text",
        "analyzer": "remove_english_stop_words"
      }
    }
  }
}
```

That's it for the built-in analyzers and creating custom analyzers. These analyzers allow you to tailor the analysis process to your specific needs, whether by using the built-in options or by creating custom configurations.

## Creating a Custom Analyzer

To create a custom analyzer, we need to follow a few steps. Let's go through them:

1. First, we need to add an object named "analysis" within the "settings" object of our index. This is where we'll configure the analyzer.

2. Inside the "analysis" object, we add another object named "analyzer." Analyzers must be declared within this object.

3. We specify the name of our custom analyzer as a key with an object as its value. For example, let's name it "my_custom_analyzer" for demonstration purposes.

4. Now comes the interesting part—configuring the analyzer. We'll define the behavior we want for our custom analyzer.

   Let's consider some text that contains HTML markup and entities. Typically, you'd want to remove these before indexing into Elasticsearch. However, for this example, let's assume they haven't been stripped.

   Analyzing this text using the "standard" analyzer would yield strange terms since it treats HTML tags and entities as separate tokens.

   To address this, we can use the "html_strip" character filter, which removes HTML tags and decodes entities. We'll modify the query to include this character filter.

5. Remove the "standard" analyzer from the query so that we can see the effect of the character filter on its own.

6. We can add a parameter named "char_filter" to our custom analyzer, which contains an array of character filter names. In this case, we'll include only the "html_strip" character filter.

7. We still need to specify a tokenizer. For simplicity, let's use the "standard" tokenizer.

8. Next, we'll add token filters. We'll start by including the "lowercase" token filter to lowercase terms.

9. We can also remove stop words by adding the "stop" token filter. By default, it removes stop words for the English language. However, we'll see how to configure it for a different language shortly.

10. As a third token filter, let's use the "asciifolding" token filter to convert special characters to their ASCII equivalents. This will allow variations in letter forms to match.

11. With our custom analyzer configured, we can create the index and test the analyzer. You can use the Analyze API to see how each part of the analyzer affects the output.

12. To use the custom analyzer in field mapping, specify its name as the value for the "analyzer" parameter, just as we did with built-in analyzers.

Congratulations! You now know how to create custom analyzers in Elasticsearch. You can tailor analyzers to suit your specific needs by combining character filters, tokenizers, and token filters. Remember that you can also configure the behavior of built-in analyzers or create custom configurations by extending them.

Sure! Here are the revised notes with explanations and code snippets:

## Creating a Custom Analyzer

To create a custom analyzer, we need to follow a few steps. Let's go through them:

1. First, we need to add an object named "analysis" within the "settings" object of our index. This is where we'll configure the analyzer.

2. Inside the "analysis" object, we add another object named "analyzer." Analyzers must be declared within this object.

3. We specify the name of our custom analyzer as a key with an object as its value. For example, let's name it "my_custom_analyzer" for demonstration purposes.

4. Now comes the interesting part—configuring the analyzer. We'll define the behavior we want for our custom analyzer.

   Let's consider some text that contains HTML markup and entities. Typically, you'd want to remove these before indexing into Elasticsearch. However, for this example, let's assume they haven't been stripped.

   Analyzing this text using the "standard" analyzer would yield strange terms since it treats HTML tags and entities as separate tokens.

   To address this, we can use the "html_strip" character filter, which removes HTML tags and decodes entities. We'll modify the query to include this character filter.

5. Remove the "standard" analyzer from the query so that we can see the effect of the character filter on its own.

6. We can add a parameter named "char_filter" to our custom analyzer, which contains an array of character filter names. In this case, we'll include only the "html_strip" character filter.

7. We still need to specify a tokenizer. For simplicity, let's use the "standard" tokenizer.

8. Next, we'll add token filters. We'll start by including the "lowercase" token filter to lowercase terms.

9. We can also remove stop words by adding the "stop" token filter. By default, it removes stop words for the English language. However, we'll see how to configure it for a different language shortly.

10. As a third token filter, let's use the "asciifolding" token filter to convert special characters to their ASCII equivalents. This will allow variations in letter forms to match.

11. With our custom analyzer configured, we can create the index and test the analyzer. You can use the Analyze API to see how each part of the analyzer affects the output.

12. To use the custom analyzer in field mapping, specify its name as the value for the "analyzer" parameter, just as we did with built-in analyzers.

Congratulations! You now know how to create custom analyzers in Elasticsearch. You can tailor analyzers to suit your specific needs by combining character filters, tokenizers, and token filters. Remember that you can also configure the behavior of built-in analyzers or create custom configurations by extending them.

## Adding an Analyzer to an Existing Index

In the previous lecture, we learned how to add a custom analyzer at index creation time. But what if you already have an existing index and want to add an analyzer to it? Let's explore how to do that.

To add an analyzer to an existing index, we can use the Update Index Settings API. This API allows us to update various settings of an index, including analyzers. The request body format is similar to the "settings" object used during index creation.

1. Start by sending a POST request to the Update Index Settings API, specifying the index you want to update:

```json
POST /your_index/_settings
```

2. In the request body, include the "analysis" object at the root level. This object follows the same format as seen in the previous lecture.

```json
POST /your_index/_settings
{
  "analysis": {
    "analyzer": {
      "new_analyzer": {
        "type": "custom",
        "tokenizer": "standard",
        "filter": ["lowercase"]
      }
    }
  }
}
```

3. If the index is currently open and serving requests, you will encounter an error stating that non-dynamic settings cannot be updated for open indices. This error occurs because some settings, including analysis settings, are considered static and can only be changed while the index is closed.

4. To resolve this, close the index by sending a POST request to the Close Index API:

```json
POST /your_index/_close
```

5. After successfully closing the index, re-send the request to update the index settings. This time, you should not encounter any errors.

6. Once the settings update is complete, you can reopen the index by sending a POST request to the Open Index API:

```json
POST /your_index/_open
```

7. With the index open again, the new analyzer is ready to be used within field mappings.

8. To verify that the analyzer has been added, you can retrieve the index settings by sending a GET request to the Get Index Settings API:

```json
GET /your_index/_settings
```

9. In the response, you will see the updated index settings, including the newly added analyzer.

It's important to note that closing and reopening an index is not specific to analyzers; it applies to any analysis-related changes such as modifying character filters, tokenizers, or token filters. While this process may temporarily make the index unavailable for indexing and searching, it can be done during maintenance windows or with proper planning.

In situations where downtime is not acceptable, an alternative approach is to reindex the documents into a new index with the desired configuration and use an index alias during the transition period.

Updating analyzers follows a similar process, requiring the index to be closed, updating the analyzer settings, reopening the index, and verifying the changes using the Get Index Settings API.

Now you know how to add analyzers to existing indices and update analyzers when necessary.

## Updating an Existing Analyzer

Sometimes you may need to update an existing analyzer. While it's best to get the analyzer configuration right the first time, circumstances may change, and updates may become necessary. In this lecture, we'll explore how to update an existing analyzer.

To demonstrate the process, we have an index with a custom analyzer that hasn't been used in a field mapping yet. Let's first add a "description" field to the index that utilizes the "my_custom_analyzer" analyzer.

1. Add the "description" field to the index mapping, specifying the "my_custom_analyzer" analyzer:

```json
PUT /your_index/_mapping
{
  "properties": {
    "description": {
      "type": "text",
      "analyzer": "my_custom_analyzer"
    }
  }
}
```

2. Index a document with the "description" field to populate the index with data.

3. Perform a search query that searches the "description" field for the term "that." Note that this query includes the "analyzer" parameter, overriding the default analyzer specified in the field mapping.

```json
GET /your_index/_search
{
  "query": {
    "match": {
      "description": {
        "query": "that",
        "analyzer": "keyword"
      }
    }
  }
}
```

4. Since the custom analyzer is configured to remove stop words, searching for the term "that" with the default analyzer would yield no results. However, by specifying the "keyword" analyzer in the query, we can prevent stop words from being removed and search for the term as-is.

5. Now let's focus on updating the existing analyzer. We can achieve this using the Update Index Settings API.

6. Send a POST request to the Update Index Settings API, specifying the analyzer's full configuration. In this case, we'll remove the "stop" token filter from the analyzer.

```json
POST /your_index/_settings
{
  "analysis": {
    "analyzer": {
      "my_custom_analyzer": {
        "type": "custom",
        "tokenizer": "standard",
        "filter": ["lowercase"]
      }
    }
  }
}
```

7. Before modifying the analyzer, we need to close the index to make the changes.

```json
POST /your_index/_close
```

8. After successfully closing the index, re-send the request to update the index settings. This time, you should not encounter any errors.

9. Once the settings update is complete, reopen the index by sending a POST request to the Open Index API.

```json
POST /your_index/_open
```

10. Verify that the analyzer has been updated by retrieving the index settings using the Get Index Settings API.

```json
GET /your_index/_settings
```

11. The response will show the updated index settings, confirming the removal of the "stop" token filter from the "my_custom_analyzer" analyzer.

12. Index another document with the same value as the first one.

13. Run the search query again. This time, both documents should match the query because the first document has been reindexed with the updated analyzer.

Updating an existing analyzer can introduce challenges. In our example, documents were analyzed using two different versions of the analyzer, which can lead to inconsistent search results. To mitigate this, you can either reindex documents into a new index with the updated analyzer or use the Update By Query API to reindex specific documents.

It's crucial to be cautious when updating analyzers as they can have significant impacts on search results. Whenever possible, strive to get your analyzer configuration right the first time. However, if updates are necessary, handle them appropriately to avoid potential issues.

Now you know how to update an existing analyzer in Elasticsearch.

## Writing Search Queries with Query DSL

Now that we understand mapping and analyzers, we can finally dive into searching for data. There are two ways to write search queries in Elasticsearch: URI search and the Query DSL. URI search involves including the search queries as a query parameter, while the Query DSL is preferred and allows us to write search queries in JSON format within the request body.

In this course, we'll focus on the Query DSL, as it provides access to all the search features and is more flexible. To write a search query using the Query DSL, we need to use the Search API with the appropriate HTTP verb and request path, as shown in the example below:

```json
POST /your_index/_search
```

Next, we'll add the request body, which should be a JSON object. We can add various parameters to configure the search request, such as pagination and sorting. The search query itself is defined within an object named "query." Let's start with the simplest possible search query, which is the "match_all" query that matches all documents:

```json
POST /your_index/_search
{
  "query": {
    "match_all": {}
  }
}
```

In this example, the "match_all" query is used without any additional parameters. This query matches all documents in the index.

After running the query, we can inspect the results. Here are some key elements to note:

- "took" indicates the time it took Elasticsearch to execute the request, measured in milliseconds.
- "timed_out" is a boolean flag indicating whether the request timed out.
- "_shards" provides information about the shards involved in executing the request, including the total number of shards, successful and failed shards, and skipped shards.
- "hits" contains the documents that matched the query, along with relevant metadata.
- Within the "hits" object, "total" represents the total number of documents that matched the query.
- "max_score" holds the highest relevance score calculated by Elasticsearch for any matching document.
- The "hits" object nested within the "hits" object contains the actual documents that matched the query, along with additional metadata for each document, such as the index name, unique identifier, relevance score, ignored fields, and the document itself stored within the "_source" key.

The example above demonstrates a basic search query that matches all documents. However, for more useful queries, we'll explore different query types that allow us to define criteria for matching documents.

Let's continue with more practical search queries.

Please note that the provided code snippets are placeholders and need to be replaced with the actual index name, field names, and query parameters relevant to your specific use case.

## Term Level Queries in Elasticsearch

In Elasticsearch, one of the query groups is called "term level queries." These queries are used to search structured data for exact values, making them suitable for filtering documents based on specific criteria such as color, brand, price, etc.

The key characteristic of term level queries is that they are not analyzed. This means that the value being searched for is used as-is to lookup values within the inverted index. Let's explore an example to understand this concept better.

Suppose we have an index of clothing products, and each document contains a field named "brand.keyword." This field stores the brand name and is mapped as a keyword field. Below is an example document along with the inverted index for the "brand.keyword" mapping:

```json
{
  "brand.keyword": "Nike"
}
```

Now, let's say we want to find all products where the brand equals "Nike." We can achieve this using a term level query because we need to search for an exact value. Here's an example of such a query:

```json
{
  "query": {
    "term": {
      "brand.keyword": {
        "value": "Nike"
      }
    }
  }
}
```

In this query, we use the "term" query to search the "brand.keyword" field for the exact value "Nike." The term level query matches our example document because the value we're searching for matches what is stored within the inverted index.

It's important to note that term level queries match exact terms and are case-sensitive. If we were to lowercase the search value, the document would no longer match. Additionally, the entire value must match, and partial matches will not result in a match. For example, searching for "Ni" would not match the document in the given example.

Term level queries can be used with various data types such as keyword, numbers, dates, etc. However, there's a common mistake that many people make: using term level queries with fields of the text data type. Let's explore why this should be avoided.

Suppose we want to find all products that contain the term "Nike" within their names. Since the "name" field is of the text data type, its values are analyzed during indexing. The inverted index for our example document would look like this:

```json
{
  "name": ["nike", "running", "shoes"]
}
```

When using a term level query with the search term "Nike," it won't yield any results. This is because the exact term "Nike" is not present within the inverted index. We're comparing an analyzed value with something that isn't analyzed, which is like comparing apples to oranges.

To clarify further, if we were to search for "nike" in lowercase, we would get a match. However, searching for the exact product name as it appears in the document would not yield any results because the field value was analyzed during indexing, causing it to be tokenized and transformed to lowercase.

Using term level queries with the text data type can lead to unexpected and unpredictable results. Comparing analyzed data with non-analyzed data can cause queries to fail to match as expected. Therefore, it's crucial to avoid using term level queries on fields with the text data type.

Instead, when searching for text values, use term level queries with fields that have the keyword data type. These fields store values as exact terms without performing analysis.

To recap, term level queries should be used for matching exact terms and are not suitable for fields with the text data type. Understanding this distinction is important to avoid unexpected results and ensure accurate search queries.

Now, let's write a couple of queries to put our knowledge into practice.

Please note that the provided code snippets are placeholders and need to be replaced with the actual index name, field names, and query parameters relevant to your specific use case.

Sure! Here's the revised text with detailed exemplar code:

## Term Level Queries in Elasticsearch

Now that we have covered the basics of term level queries, let's take a closer look at them. One of the most important term level queries is the "term" query, which you briefly saw in the previous lecture. Let's see it in action.

I have prepared the basic structure of a search query, as you've seen before. Let's add a term query to it.

```json
{
  "query": {
    "term": {
      "tags.keyword": "Vegetable"
    }
  }
}
```

In this query, we use the term query to search the "tags.keyword" field for the exact value "Vegetable." Notice that we use the keyword mapping instead of the text mapping. This is because term level queries are not analyzed and are used for exact matching.

Even though the test data specified arrays for the "tags" field, we don't need to handle that complexity within search queries. Elasticsearch automatically handles multi-valued fields, so we simply enter the name of the field, and everything is handled automatically. In this example, a document will match if it contains the "Vegetable" tag.

Let's run the query.

As you can see, it doesn't match anything. Upon closer inspection, we realize that all the product tags begin with a capital letter. Let's correct that and try again.

And there we go! This demonstrates that term level queries are case-sensitive.

Apart from searching for text values, we can also search for other data types. Here are a couple of examples:

- Searching for a boolean value (true or false) to match active products:

```json
{
  "query": {
    "term": {
      "active": true
    }
  }
}
```

- Searching for numeric values (integers, doubles, or floating points) to match products that are almost sold out:

```json
{
  "query": {
    "term": {
      "stock_quantity": 1
    }
  }
}
```

- Searching for dates, with or without the time part, to match a specific date:

```json
{
  "query": {
    "term": {
      "created_at": "2022-01-01"
    }
  }
}
```

So far, the term queries you've seen were written using a shorthand syntax. However, there's a more explicit and verbose syntax available, which you might prefer for improved readability. Here's an example:

```json
{
  "query": {
    "term": {
      "tags.keyword": {
        "value": "Vegetable",
        "boost": 1.0,
        "case_insensitive": false
      }
    }
  }
}
```

In this explicit syntax, you can specify additional parameters for the term query. For example, the "case_insensitive" parameter allows you to perform case-insensitive searches by setting it to true. However, note that this parameter is only available in recent Elasticsearch versions.

Let's test it by searching for the tag in lowercase letters:

```json
{
  "query": {
    "term": {
      "tags.keyword": {
        "value": "vegetable",
        "case_insensitive": true
      }
    }
  }
}
```

Unlike the first time we searched for an all-lowercase tag, the query now matches some documents.

So far, we've only searched for a single term. If we want to search for multiple terms, there's a variation of the term query named "terms" that serves that purpose. It works in a similar way, but instead of a single value, we provide an array of values.

Let's adjust the first query to search for multiple terms:

```json
{
  "query": {
    "terms": {
      "tags.keyword": ["Soup", "Meat"]
    }
  }
}
```

In this query, the document will match if it contains at least one of the supplied values ("Soup" or "Meat").

Let's run it and scroll through the results to see documents containing either of the tags (or both, if we're lucky). Keep in mind that only the first ten documents are returned by default.

That covers the basics of searching for exact terms in Elasticsearch using term level queries. Remember to use these queries with keyword mappings and not full-text fields to ensure accurate results.

Please note that the provided code snippets are placeholders and need to be replaced with the actual index name, field names, and query parameters relevant to your specific use case.

## Retrieving Multiple Documents Based on IDs

Earlier in the course, I showed you how to retrieve a single document based on its identifier. In this short lecture, I want to show you how to use a term level query to retrieve multiple documents at once based on their IDs. In both cases, we are querying the value of a document's `_id` field.

The name of the query we'll use is "ids". Let's add that to the partial query structure that I have prepared:

```json
{
  "query": {
    "ids": {
      "values": ["1", "2", "3"]
    }
  }
}
```

In this example, we specify the IDs as an array of values within the "values" parameter. Let's retrieve three documents using this query.

Now, let's run the query.

Within the results, we can see that three documents matched the query. These documents are returned within the "hits" key.

Note that not all IDs are required to match. The query simply returns any documents that are found with the specified IDs. So if you supply ten IDs for the query, the results will contain between zero and ten documents.

In situations where you are unsure whether the IDs exist within your index, you may want to compare the number of documents matched by the query with the number of IDs you supplied.

Using the "ids" query is particularly useful when you are using the same identifiers for your Elasticsearch documents as in a relational database, for instance. The "ids" query makes it easy to retrieve specific documents because you already know their IDs.

That's all for this lecture.

## Prefix, Wildcard, and Regular Expression Queries

In addition to exact matches, term level queries also allow for more flexible searching with prefix queries, wildcard queries, and regular expression queries. These queries provide additional options for pattern matching, but it's still important to use them with keyword fields for consistency. Let's explore each query type in detail.

### Prefix Query

The prefix query allows us to search for documents where the value of a field starts with a specific prefix. The syntax is straightforward. Here's an example of a prefix query that searches for documents where the value of the `name.keyword` field begins with "Past":

```json
{
  "query": {
    "prefix": {
      "name.keyword": "Past"
    }
  }
}
```

When we run this query, we can see that the matching documents include words like "Pastry" and "Pasta." It's important to note that the prefix must appear at the beginning of the term. Even if a word like "Pasta" appears within a term, it will not match because the prefix query only matches the beginning of the term.

If we have a `tags` field that contains tags such as "Pasta," "Paste," and "Pastry," it might be more appropriate to query that field instead of relying on the prefix appearing at the beginning of the product name. This would yield more consistent results, as the word "Pasta" could appear anywhere within the product name. By querying the `tags` field, we can match more products. 

### Wildcard Query

The wildcard query allows for searching with wildcard characters. There are two wildcard characters available: the question mark `?` and the asterisk `*`. The question mark matches any single character, while the asterisk matches any character zero or more times. Placing a wildcard at the beginning of a pattern can have significant performance implications, so it's generally advised to avoid doing so unless necessary.

Here are a few examples of wildcard patterns and their matching terms:

- "Pa?try" matches "Pastry" and "Pasta"
- "Bee*" matches "Beets," "Beer," and "Beef"

When using wildcard queries, it's important to note that they operate on terms, not on individual words within a field. The values in the field are stored as single terms, so even if a field value contains multiple words, it will be treated as a single term. 

### Regular Expression Query

The regular expression query, named `regexp`, allows for more complex pattern matching using regular expressions. Regular expressions are powerful patterns used to match strings. While the wildcard query also uses patterns, the `regexp` query enables us to define more complex patterns.

Here's an example of a regular expression pattern:

```regex
^Bee[r|f]+$
```

This pattern matches any string that starts with "Bee" followed by one or more occurrences of the letters "r" or "f." Parentheses form a group, and the pipe symbol serves as an OR operator. We can also make the pattern more dynamic by including a character set, allowing any letter to follow the "Bee" prefix.

It's important to remember that a regular expression pattern must match the entire term for a document to be considered a match. For example, the pattern `^Bee[r|t]$` matches terms like "Beer" and "Beet," but not "Beetroot" because the pattern only matches part of the term.

When using regular expressions, Elasticsearch relies on Apache Lucene's regular expression engine. While the syntax is similar to other regular expression engines, there are a few differences. Anchor operators, such as the caret `^` and dollar `$` symbols, are not supported. Instead, the pattern must match the entire string.

Here's an example of a `regexp` query using the previously mentioned pattern:

```json
{
  "query": {
    "regexp": {
      "tags.keyword": "^Bee[r|f]+"
    }
  }
}
```

When running this query, it matches the "Beef" and "Beer" tags.

By default, term level queries are case sensitive. However, all three queries—prefix, wildcard, and regexp—support a `case_insensitive` parameter that can be used to perform case-insensitive searches. Here are examples of each query with the `case_insensitive` parameter set to `true`:

- Prefix query:
  ```json
  {
    "query": {
      "prefix": {
        "name.keyword": {
          "value": "Past",
          "case_insensitive": true
        }
      }
    }
  }
  ```

- Wildcard query:
  ```json
  {
    "query": {
      "wildcard": {
        "name.keyword": {
          "value": "Pa*",
          "case_insensitive": true
        }
      }
    }
  }
  ```

- Regexp query:
    ```json
  {
    "query": {
      "regexp": {
        "name.keyword": {
          "value": "^P[a-z]+",
          "case_insensitive": true
        }
      }
    }
  }
    ```

That concludes this lecture. In the next one, we will explore full-text queries.

Certainly! Here's the revised text with detailed exemplar code:

## Searching for Documents Based on Field Existence

In Elasticsearch, we can search for documents based on whether or not they contain a value for a specific field using the `exists` query. This query is similar to the `IS NOT NULL` condition in relational databases. To use the `exists` query, we simply specify the name of the field.

Here's an example of an `exists` query:

```json
{
  "query": {
    "exists": {
      "field": "tags.keyword"
    }
  }
}
```

When running this query, it's surprising to see that it only matches 554 documents, even though all the documents contain a value for the `tags` field. The reason is that the `exists` query matches documents that contain an indexed value for a field. If we supply an empty value (NULL or an empty array) for a field during indexing, the value is stored in the `_source` object but not indexed. Only non-empty values are indexed.

In our dataset, some documents have an empty array as the value for the `tags` field. These documents do not have any values indexed for the field. Let's take a closer look at an example:

- Document #1: Contains a value for both the `name` and `tags` fields. The values are analyzed and indexed into the inverted index.
- Document #2: Also contains a value for both the `name` and `tags` fields. However, the `tags` field has an empty array as its value. Since an empty array is treated as if no value was provided, nothing is added to the field's inverted index.

If we run an `exists` query on the `tags` field, only document #1 will match.

Besides empty values, there are a few other reasons why a document might not have an indexed value for a field:

- If a `null_value` parameter is specified in the field's mapping and a value of `NULL` is provided, the value will be indexed. This allows the document to match an `exists` query.
- If no value is provided for a field during indexing, the field will be missing from the indexing request, and no value will be indexed.
- The `index` mapping parameter can be set to `false` in the field's mapping, indicating that the field's values should not be indexed. This is commonly used for numeric fields that are used for aggregations rather than filtering.
- The `ignore_above` parameter can be used to specify a maximum length for keyword fields. If a value exceeds this length, it is ignored for indexing. The default value is 256 for keyword fields with dynamic mapping. However, for text fields, the value will still be indexed even if it exceeds the `ignore_above` threshold.
- The `ignore_malformed` parameter can be set to `true` in the field's mapping. If a value of an incompatible data type is provided, such as indexing a string into a numeric field, the value will be ignored (not indexed). If the parameter is not specified, the indexing request would fail.

To search for documents that do not contain an indexed value for a field, there is no dedicated query for that purpose. Instead, we can use the `bool` query and combine it with the `must_not` parameter. Here's an example:

```json
{
  "query": {
    "bool": {
      "must_not": {
        "exists": {
          "field": "tags.keyword"
        }
      }
    }
  }
}
```

In this query, the `exists` query is added to the `must_not` parameter of the `bool` query. This means that a document will only match if it does not have a value indexed for the `tags.keyword` field.

When running this query, we can see that it matches 446 documents, while the previous query matched 554 documents. If we scroll through the results, we will see that the documents all contain an empty array for the `tags` field, indicating that no value was indexed.

That concludes this lecture. In the next one, we will explore the `match` query for full-text searching.

## Full Text Queries

Full text queries are used to search through unstructured text data, such as blog posts, news articles, comments, etc. These queries are designed to find documents that contain specific words or phrases within their content. Unlike term level queries that are used for exact matches on structured data, full text queries are used for searching unstructured text data.

Let's consider an example where we have an index called "posts" that contains various blog posts. Here's an example document structure:

```json
{
  "title": "Introduction to Elasticsearch",
  "body": "Elasticsearch is a distributed, scalable search and analytics engine."
}
```

In this example, the "title" and "body" fields are of the "text" data type. If we search for the word "Elasticsearch," this document would match because the word appears in both the title and body fields.

The main difference between full text queries and term level queries is that the query itself is analyzed. When processing the query, Elasticsearch inspects the field mapping for the specified field. If an analyzer is configured for the field, Elasticsearch uses that analyzer. Otherwise, it defaults to the standard analyzer. The query is then run through the analyzer, applying the same analysis process used during document indexing.

This analysis step is crucial to ensure that the query and indexed values are compared correctly. For example, if the term "Elasticsearch" is indexed as lowercase, searching for "ELASTICSEARCH" in uppercase would not match anything. By analyzing the query using the same analyzer as the indexed values, both are transformed consistently.

Full text queries use the analyzed term to perform a lookup within the inverted index. If a match is found, the corresponding documents are considered as matches for the query and returned in the results.

The fact that full text queries are analyzed is the primary difference between full text queries and term level queries. Term level queries are not analyzed and are used for exact matching. In contrast, full text queries are analyzed, making them suitable for searching unstructured text data. Therefore, full text queries should not be used with fields of the "keyword" data type because keyword fields store non-analyzed values, while full text queries require analyzed values.

To summarize, full text queries are used to search through unstructured text values, such as blog posts, emails, news articles, etc. They are not used for exact matching but rather for finding documents where specific terms appear. The analysis process ensures consistent comparison between the query and indexed values. Remember that full text queries should not be used with keyword fields that store non-analyzed values.

Now that we understand the basics of full text queries, let's write an example query.

## The Match Query

The match query is one of the most commonly used full text queries in Elasticsearch. It returns documents that contain one or more specified terms. The inner workings of the match query follow the same principles we discussed in the previous lecture. The query is analyzed, and the resulting terms are looked up in the field's inverted index.

Let's write an example query using the match query to search the "name" field for the word "pasta."

```json
{
  "query": {
    "match": {
      "name": "pasta"
    }
  }
}
```

In this example, the query matches 12 products that contain the word "pasta" within their names. It's important to note that the word "pasta" can appear anywhere within the field values since we are no longer searching for exact matches.

To demonstrate that the value is analyzed, let's change the query to uppercase letters.

```json
{
  "query": {
    "match": {
      "name": "PASTA"
    }
  }
}
```

Surprisingly, the results remain the same. Internally, the term "PASTA" is run through the analyzer, which includes the lowercase token filter. Both versions of the query search for "pasta" in lowercase letters, matching the way the term is stored in the inverted index.

So far, our queries have consisted of single words. Let's now explore how the match query handles multiple words, which is common in search scenarios. Instead of searching for just "pasta," let's search for "chicken" as well.

Before running this query, let's understand how it works. The value is analyzed, resulting in two terms: "pasta" and "chicken." Both terms are looked up in the inverted index to find documents that contain either or both of them.

```json
{
  "query": {
    "match": {
      "name": "pasta chicken"
    }
  }
}
```

When we run the query, the results will include products that contain both terms, as well as those containing only one of them.

By default, the match query has an "OR" operator, which means a document matches if either or both terms appear within the field's value. If we explicitly set the operator parameter to "AND," both terms are required for a document to match.

Let's modify our previous query to use the "AND" operator:

```json
{
  "query": {
    "match": {
      "name": {
        "query": "pasta chicken",
        "operator": "AND"
      }
    }
  }
}
```

In this example, we restructured the query to include an object as the value for the "name" field. We added the "query" parameter with the desired value and the "operator" parameter set to "AND."

When we run the query, only documents containing both terms within the "name" field will be returned.

The match query is a fundamental and powerful query in Elasticsearch, and it's likely to be used for most full text searches. It also has advanced parameters that provide even greater flexibility, which we will cover in a later lecture.

One important note is that the match query can also be used when searching for numbers, dates, and boolean values. It offers forgiveness in terms of the search input, making it suitable for search fields. However, if the search is not based on user input, it's preferable to use term level queries for these data types.

That concludes this lecture. I'll see you in the next one!

## Relevance Scoring in Full Text Queries

In the previous lecture, I ran a query that searched for both "pasta" and "chicken." You can see the query and its results on your screen. You might have noticed that the documents at the top of the results contain both of the terms. This is because there is an important concept we haven't discussed yet: relevance scoring.

Apart from the match query, we have only covered term level queries thus far. You may have noticed that the documents matching these queries all had a value of 1.0 for the `_score` field. I didn't mention it earlier because relevance scoring is generally not applicable to term level queries. These queries evaluate a condition that is either true or false, resulting in a document either matching or not matching the query. There are exceptions, but this is generally the case.

However, with full text queries, we are no longer performing exact matching. It's not just about whether or not a document matches; we also care about how well it matches. Consider the search results on Google, for instance. We expect the best results to be at the top, not on page 201.

The same concept applies to full text queries in Elasticsearch. Search results are sorted based on the relevance scores, with the matches that have the highest values for the `_score` field appearing at the top. In other words, the results are sorted in descending order based on the `_score` meta field.

This explains why documents containing both terms from the search query appeared first in the results. They were scored higher because they matched the query better than the documents that contained only one of the terms.

It's important to note that the specific numbers you see for the `_score` field may vary. Relevance scoring is a complex process that considers numerous factors, so exact score values may differ. We will explore how Elasticsearch calculates these scores in more detail later in the course.

For now, it's sufficient to understand how relevance scoring works at a high level. Full text queries are analyzed, and the resulting terms are looked up in the inverted index for the field. Elasticsearch then calculates relevance scores for each matching document. Once the scores are calculated, the documents are sorted based on their scores to form the query results.

This is just a high-level overview of relevance scoring. We will delve deeper into the topic in subsequent lectures.

That concludes the explanation of relevance scoring for now. Let's continue with the course.

## Multi-match Query for Searching Multiple Fields

In the previous lecture, we saw the match query in action, which was great for searching a single field. But what if we want to search multiple fields? One way to accomplish this is by using a query named multi_match, which we'll explore in this lecture.

The syntax for the multi_match query is straightforward. Let me type out a query that searches both the name and tags fields for the term "vegetable."

```json
{
  "query": {
    "multi_match": {
      "query": "vegetable",
      "fields": ["name", "tags"]
    }
  }
}
```

When we run this query, we can see that several documents match the query. If we examine the first document, we can see that the word "vegetable" appears within the name field. Similarly, for the second document, it appears within the tags field. Therefore, we have successfully searched both fields simultaneously. It's important to note that a document matches if it contains the term in at least one of the specified fields.

That was easy, right? However, don't be fooled because the multi_match query is actually a very advanced query. Let's take a closer look at what else it has to offer.

One useful feature is the ability to adjust the relevance scoring per field to control the importance of fields in the search. For example, if we want to boost documents where the term appears in the name field, we can apply a relevance boost to that field. To do this, we specify a caret symbol after the field name, followed by a number. For instance, to double the relevance score for documents where the term appears in the name field, the query would look like this:

```json
{
  "query": {
    "multi_match": {
      "query": "vegetable",
      "fields": ["name^2", "tags"]
    }
  }
}
```

In this case, the relevance scores for documents that match the term in the name field will be multiplied by two. Running the query, we can see that the relevance score for the first document has indeed doubled.

Now let's take a closer look at how the multi_match query works internally. Elasticsearch actually rewrites the query to construct separate match queries for each specified field. If at least one of these match queries matches for a document, then that document will be part of the results. This is a simplified explanation, but it captures the essence of the process.

Regarding relevance scoring, the multi_match query has a `type` parameter that can be used to adjust how relevance scores are calculated. However, for now, let's focus on the default behavior. By default, the relevance score of the best matching field is used for the document. Suppose we search the name and description fields for two terms, "vegetable" and "broth." The query would be translated into two match queries internally. In the example document, we can see that the name field contains both terms, while the description field only contains the term "vegetable." The Elasticsearch relevance algorithm assigns a higher score to the name field. This behavior applies to the other documents as well.

Please note that the relevance scores I assigned are arbitrary and should not be considered as real-world values.

By default, the multi_match query evaluates the scores for each field in a document and selects the highest score. In this case, the highest score belongs to the name field. These relevance scores become the `_score` values within the search results, indicating the relevance of the documents.

Now, I want to show you a way to adjust this default behavior using something called a tie breaker. By default, multiple fields are searched, but only the highest-scoring field is considered for relevance scoring. However, we might want to "reward" documents where multiple fields match. By defining a tie breaker, we can incorporate all matching fields into the relevance scores for the documents. Let's look at an example using the same query as before, but with the tie_breaker parameter:

```json
{
  "query": {
    "multi_match": {
      "query": "vegetable",
      "fields": ["name", "description"],
      "tie_breaker": 0.3
    }
  }
}
```

In the example document, I added relevance scores for each of the two fields. By default, the highest score (from the name field) would be selected, resulting in a score of 12.69. However, with the tie breaker, the behavior is as follows: the highest score is still selected (from the name field), giving a score of 12.69. For every other matching field, Elasticsearch takes those relevance scores and multiplies them by the tie breaker value (0.3 in this case). For the description field, the score of 8.51 would be multiplied by 0.3, resulting in 2.55. This number is then added to the relevance score of the best matching field. The resulting score becomes the relevance score for the document.

In a scenario where we search four fields and three of them match, each document receives a relevance boost for each additional field that matches besides the best matching field. This accounts for the relevance of terms appearing in fields with lower scores, indicating some degree of relevance to consider. Depending on your use case, this behavior may or may not be desired, and you can adjust the tie breaker value accordingly.

That covers the basics of the multi_match query. Be sure to consult the Elasticsearch documentation if you're curious about the more advanced ways to adjust relevance scoring. I'll see you in the next lecture!

## Phrase Searches with the match_phrase Query

Earlier, we covered the match query, which matches a value if at least one of the specified terms appears anywhere within the field value. The terms can appear in any order. Let's take a look at an example:

```json
{
  "query": {
    "match": {
      "description": "Fanta Zero"
    }
  }
}
```

In this example, searching for both "Fanta Zero" and "Zero Fanta" will yield the same results. The terms do not have to be adjacent. For phrase searches, however, the order of the words matters, unlike the match query.

Phrase searches are performed using the match_phrase query in Elasticsearch. The match_phrase query is analyzed in the same way as the match query, usually with the standard analyzer. Let's go through some example documents and evaluate whether or not they are matched by a phrase query.

While the first document contains all the terms we are searching for, it's not matched by the query. This is because the terms are not adjacent; there are two words in-between them. For a phrase to match, the terms must appear in the correct order and with no other terms in-between.

The next document is not matched either because one of the terms is missing, and the order of the terms is different. In phrase searches, it is a requirement that all terms are present. Additionally, there are two other terms in-between the matching ones.

The third document also doesn't match because the terms appear, but not in the correct order. Note that the values shown here would also be analyzed and stored within an inverted index. Therefore, parentheses or any other symbols make no difference in matching; only the order of the terms matters.

The fourth and fifth documents do match because the phrases appear within the field values. All terms are adjacent and in the correct order, matching the phrase we are searching for.

So, how do these phrase searches work? Elasticsearch needs to efficiently find the documents where the terms appear in a specific order, keeping track of term positions within field values. Elasticsearch stores additional information in the inverted indices to accomplish this. When a string is indexed into a text field, the analyzer records the position of each term. These positions are then stored within the field's inverted index.

During a phrase query, Elasticsearch uses these positions to check if the terms appear in the correct order. It performs a lookup within the inverted index to identify the documents containing the terms and then verifies if the terms appear as a phrase, meaning next to each other in the correct order. This is determined by checking the positions and ensuring they are in increments of one.

To illustrate this, let's consider the following query:

```json
{
  "query": {
    "match_phrase": {
      "description": "guide to elasticsearch"
    }
  }
}
```

Based on the analyzed query, Elasticsearch performs a lookup within the inverted index for the description field to identify the documents containing the terms. In this example, both documents contain all three terms. Based on the term positions, Elasticsearch determines whether the terms appear as a phrase. If the positions of the term "guide" were three and five, respectively (one greater than those of the "elasticsearch" term), the documents would match the phrase query.

Here's an example of a phrase query that does match a document:

```json
{
  "query": {
    "match_phrase": {
      "description": "guide elasticsearch"
    }
  }
}
```

In this case, the positions of the terms "guide" and "elasticsearch" satisfy the phrase condition, and the document matches the query.

Now that you've seen the concept of phrase queries, let's run some queries to further illustrate their usage. We have four simple phrase queries prepared. Let's quickly run them one by one.

The first query searches for "mango juice" but doesn't match anything. The second query searches for the phrase "juice mango," which matches one document. The terms are the same, but they are in the correct order as they appear within the document. Notice how the hyphen doesn't affect the matching because it was dropped during the analysis process. Similarly, adding symbols within queries won't have any effect on matching.

Lastly, let's search the description field for a phrase consisting of three words. This query matches one document as well. The phrase appears in the middle of the value for the description field.

These were simple examples to demonstrate phrase queries in action. Now you have a solid understanding of how to use the match_phrase query and how it works.

That's all for this lecture!

## Compound Queries: Wrapping Leaf Queries

We have just covered both term level queries and full text queries. However, I haven't mentioned that all of these queries are referred to as leaf queries. A leaf query is a query that searches for a value within one or more fields and can be used by itself. For example, the term query and the full text queries we covered fall into this category.

On the other hand, a compound query is a query that wraps other queries to combine them logically. Compound queries orchestrate other queries to produce a result. Let's take a simple example to understand the difference. Suppose we want to search for products that contain the "Alcohol" tag and are almost sold out. This would involve two leaf queries: a term query and a range query.

In Elasticsearch, we can only define a single query at the top level of our request. This means that these two leaf queries need to be wrapped within a compound query. Compound queries can contain one or more leaf queries or other compound queries.

To combine multiple queries, we need to wrap them within a compound query. Advanced queries can be nested further, such as nesting a compound query within another compound query. This allows us to write powerful and complex queries.

Here's a quick example to illustrate this concept. Let's say we want to find products with the "Alcohol" tag that are either sold out or inactive. In SQL, this could be represented as:

```sql
SELECT * FROM products
WHERE tag = 'Alcohol' AND (status = 'Sold Out' OR status = 'Inactive')
```

In Elasticsearch, this query would consist of three leaf queries:

1. Term query for the "Alcohol" tag.
2. Term query for the "Sold Out" status.
3. Term query for the "Inactive" status.

To construct the boolean logic, we would wrap these leaf queries within compound queries. The resulting Elasticsearch query would look something like this:

```json
{
  "query": {
    "bool": {
      "must": [
        {
          "term": {
            "tag": "Alcohol"
          }
        }
      ],
      "should": [
        {
          "term": {
            "status": "Sold Out"
          }
        },
        {
          "term": {
            "status": "Inactive"
          }
        }
      ]
    }
  }
}
```

As you can see, the compound query in this example is a boolean query with the `must` and `should` clauses. It contains both leaf queries and another compound query. This enables us to write powerful and complex queries by combining multiple conditions.

Now that you understand the concept of compound queries and how they wrap leaf queries, let's explore some compound queries in more detail.

That's all for this lecture!

## The Bool Query: Combining Multiple Conditions

Now that you understand what compound queries are, let's take a look at one of the most commonly used compound queries: the bool query. "Bool" is short for "boolean," and as the name suggests, this query is used in situations where you have more than one condition. Each condition is expressed as a clause, which is just another word for a query in this context. The bool query contains other queries, which makes it a compound query.

These clauses are defined within occurrence types, which are used to define boolean logic. Let's start writing some queries to see how the bool query works.

One of the occurrence types we can use is "must," which contains zero or more query clauses. Within this array, we can add queries that must match. These can be any queries, including the ones we have seen so far. Let's start with a simple example: matching documents that contain the "Alcohol" tag. We can use the term query for this purpose.

```json
{
  "query": {
    "bool": {
      "must": [
        {
          "term": {
            "tag": "Alcohol"
          }
        }
      ]
    }
  }
}
```

Running this query will return documents that have the "Alcohol" tag.

The result of this query is equivalent to the following SQL query:

```sql
SELECT * FROM products
WHERE tag = 'Alcohol';
```

Next, let's move on to the "must_not" occurrence type. As the name suggests, this is where we can add query clauses that must not match. Any document that matches any of these clauses will not be included in the results. Let's expand our query by excluding documents with the "Wine" tag using a simple term query.

```json
{
  "query": {
    "bool": {
      "must": [
        {
          "term": {
            "tag": "Alcohol"
          }
        }
      ],
      "must_not": [
        {
          "term": {
            "tag": "Wine"
          }
        }
      ]
    }
  }
}
```

Running this query will match documents with the "Alcohol" tag that do not have the "Wine" tag. 

The result of this query is equivalent to the following SQL query:

```sql
SELECT * FROM products
WHERE tag = 'Alcohol' AND tag != 'Wine';
```

With the bool query, we can already build powerful queries. However, there is more to explore. Let's move on to the next occurrence type: "should." Clauses within this occurrence type are not required to match, but if they do, they will boost the relevance scores of the matching documents.

Let's expand our query further. Suppose we are interested in beer specifically and want to score beers higher than other kinds of products without excluding them. We can achieve this by adding a query clause that matches beers. Since there is a tag for beers, we can use a term query for that as well.

```json
{
  "query": {
    "bool": {
      "must": [
        {
          "term": {
            "tag": "Alcohol"
          }
        }
      ],
      "must_not": [
        {
          "term": {
            "tag": "Wine"
          }
        }
      ],
      "should": [
        {
          "term": {
            "tag": "Beer"
          }
        }
      ]
    }
  }
}
```

Running this query will prioritize beers in the search results. The documents that match the "Beer" tag will receive a relevance boost.

We can further improve this query by boosting the relevance scores of documents where the term "beer" appears in other fields, such as the name or description fields. We can achieve this by adding match queries for the name and description fields. Since we are now searching through unstructured text, we can use full-text queries.

```json
{
  "query": {
    "bool": {
      "must": [
        {
          "term": {
            "tag": "Alcohol"
          }
        }
      ],
      "must_not": [
        {
          "term": {
            "tag": "Wine"
          }
        }
      ],
      "should": [
        {
          "term": {
            "tag": "Beer"
          }
        },
        {
          "match": {
            "name": "beer"
          }
        },
        {
          "match": {
            "description": "beer"
          }
        }
      ]
    }
  }
}
```

Running this query will prioritize documents that have the term "beer" in their name or description fields, in addition to matching the "Alcohol" tag and excluding the "Wine" tag.

Now that we have covered all the occurrence types, let's recap:

- The "must" clauses are required to match and influence the relevance scores of documents. Place criteria that documents must fulfill here if you want them to contribute to the relevance scores of matching documents.
- The "must_not" clauses are used to filter out documents. The query clauses within this occurrence type must not match. They don't affect relevance scores and can be cached by Elasticsearch.
- Each matching "should" clause boosts the relevance scores of documents. This is useful for queries that are not required to match. The more "should" clauses match, the higher the relevance score. You can configure the minimum number of clauses required to match using the "minimum_should_match" parameter.
- The "filter" clauses must match and are similar to "must" clauses. However, "filter" clauses ignore the relevance scores of matching documents. Placing query clauses within the "filter" occurrence type can improve query performance as Elasticsearch doesn't need to calculate relevance scores or order the results. The results can be cached and used for subsequent executions of the query.

Remember that compound queries can be nested, and you can combine them in various ways to construct powerful and flexible queries.

Now, let's explore some example queries to further illustrate these concepts:

**Example 1: Find products with 100 or fewer items in stock, tagged with "Beer" or containing "Beer" in their names.**

```json
{
  "query": {
    "bool": {
      "filter": [
        {
          "range": {
            "in_stock": {
              "lte": 100
            }
          }
        }
      ],
      "should": [
        {
          "term": {
            "tag": "Beer"
          }
        },
        {
          "match": {
            "name": "beer"
          }
        }
      ]
    }
  }
}
```

**Example 2: Find products tagged with "Beer" that have 100 or fewer items in stock. Additionally, the term "Beer" should appear in the product name or description.**

```json
{
  "query": {
    "bool": {
      "filter": [
        {
          "term": {
            "tag": "Beer"
          }
        },
        {
          "range": {
            "in_stock": {
              "lte": 100
            }
          }
        }
      ],
      "should": [
        {
          "match": {
            "name": "Beer"
          }
        },
        {
          "match": {
            "description": "Beer"


          }
        }
      ]
    }
  }
}
```

Feel free to run these example queries and experiment with different combinations to further understand the bool query and compound queries in Elasticsearch.

That's all for this lecture! If you have any questions, feel free to ask.

## Query Execution Contexts: Query and Filter

In this lecture, we'll discuss query execution contexts. You actually saw an example of it in the previous lecture, but let's dive deeper into the concept now.

In Elasticsearch, there are two contexts in which queries can be executed. The first one is the query context. This is what you have been using so far, with one exception that we'll discuss shortly.

The query context determines whether or not a document matches the query clause. Additionally, it asks the question: "How well does this document match?" Relevance scoring is involved in determining the answer to this question. Relevance scores are floating-point numbers that represent the relevance of a document to the query. These scores are available in the `_score` metadata field for each matching document. Higher relevance scores indicate a better match, meaning the document is more relevant to the query. The results returned by the Search API are sorted by relevance scores in descending order, with the most relevant documents appearing first.

So when is a query clause executed in the query context? To answer that question, let's look at a simple search query:

```json
{
  "query": {
    "match": {
      "title": "elasticsearch"
    }
  }
}
```

The key named "query" at the root of the request body indicates that the query clauses nested within this key are executed in the query context, meaning that documents are rated based on relevance.

Now, let's talk about the second execution context, which is the filter context. Query clauses that are run in the filter context answer the question: "Does this document match?" In the filter context, it's a simple yes or no question. Either a document matches the criteria or it doesn't. No relevance scores are calculated in the filter context, so Elasticsearch doesn't evaluate the quality of the match. The filter context is primarily used for filtering data, especially structured data such as dates, numbers, and the keyword data type. Relevance scoring is unnecessary or irrelevant for such filtering. The benefit of the filter context is that Elasticsearch doesn't need to spend resources on calculating relevance scores, and the results can be cached.

The concept of query execution contexts might sound familiar because we discussed it in the previous lecture in the context of the bool query. Consider the following query:

```json
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "title": "elasticsearch"
          }
        }
      ],
      "filter": [
        {
          "range": {
            "timestamp": {
              "gte": "2022-01-01"
            }
          }
        }
      ],
      "must_not": [
        {
          "term": {
            "status": "archived"
          }
        }
      ]
    }
  }
}
```

The bool query runs in the query context, as indicated by the "query" key. However, query clauses within both the "filter" and "must_not" occurrence types run in the filter context. This means that these clauses don't affect relevance scoring and can be cached.

In situations where you don't require relevance scoring, it's a good optimization to move query clauses from the "must" occurrence type to the "filter" occurrence type. By doing so, you can change the execution context to the filter context.

Note that only a few queries support changing the execution context to the filter context, and they generally have a parameter named "filter" to specify it. The bool query is a common example where you can utilize the filter context. The same concept can be applied within aggregations, but we'll cover that later. 

To summarize, by default, queries are executed in the query context unless specified otherwise. Relevance scores are calculated within the query context, answering the question "How well does this document match?" For some queries, it's possible to change the execution context to the filter context. In the filter context, no relevance scores are calculated, and the question is simply "Does this document match?" Not calculating relevance scores improves performance, and query clauses within the filter context can be cached for even better performance. When filtering documents, consider whether you need relevance scoring or simply want to filter out documents that don't match the criteria. If relevance scoring is unnecessary, use the filter context whenever possible. This optimization is particularly important for large indices.

These are the two execution contexts in Elasticsearch, typically used within the bool query and the filter aggregation, which we will cover later.

If you have any questions or need further clarification, feel free to ask!

## Boosting Query: Decreasing Relevance Scores

In this lecture, we'll explore the boosting query, which allows us to decrease the relevance scores of documents. Consider the following query:

```json
{
  "query": {
    "boosting": {
      "positive": {
        "match": {
          "name": "juice"
        }
      },
      "negative": {
        "match": {
          "name": "apple"
        }
      },
      "negative_boost": 0.5
    }
  },
  "size": 20
}
```

This query searches for products that contain the term "juice" within their names. We want to decrease the relevance scores of documents that also contain the term "apple." The boosting query consists of two parts: a "positive" and a "negative" query clause. The "positive" query clause, defined within the "positive" parameter, is required to match, similar to the "must" occurrence type in the bool query. We add the same query clause that matches all juice products.

Within the "negative" parameter, we specify a query clause that reduces the relevance scores of matching documents. In this case, since we don't like apple juice, we search for the term "apple" within the negative query clause. Since the negative query is run in the context of the results from the positive query, we only need to search for "apple" here.

So, the boosting query matches any documents that match the positive query clause. Documents that also match the negative query clause have their relevance scores reduced. This is the opposite of the "should" occurrence type in the bool query, where matching documents receive a relevance boost.

Now, let's add the "negative_boost" parameter. This parameter accepts a floating-point number between 0 and 1.0. It acts as a modifier for documents that match the negative query clause. When a document matches the boosting query, there are two scenarios:

1. If a document only matches the positive query clause, its relevance score remains intact. The relevance score is the one calculated by the match query defined within the positive parameter. These scores are the unmodified scores.

2. If a document matches both the positive and negative query clauses, its relevance score is multiplied by the negative_boost value. In this example, the negative_boost value is 0.5, so the relevance scores of these documents are halved.

By running this query, we no longer see the "Apple Juice" product at the top of the results. If we scroll to the bottom, we can find all the apple juice products. These documents matched the negative query clause and had their relevance scores reduced.

The boosting query allows us to decrease the relevance of some documents, which cannot be achieved with the bool query. In this example, we searched for juice products and decreased the relevance of apple juice.

It's important to note that the positive query clause is required, so we need to add something to it. In cases where we don't want to narrow down or filter the documents in the positive parameter, we can simply add a match_all query.

The examples shown thus far have been relatively simple. However, in real-world scenarios, queries can become more complex. Let's look at a couple of more advanced examples for reference. These examples are fictional and not based on our test data.

Suppose we have an imaginary recipe dataset. We want to boost recipes with pasta and decrease the relevance of recipes with bacon. Both preferences include all products, so they can be considered preferences rather than requirements. Here are two simple queries:

1. Boost recipes with pasta:

```json
{
  "query": {
    "boosting": {
      "positive": {
        "match": {
          "ingredients": "pasta"
        }
      },
      "negative": {
        "match": {
          "ingredients": "bacon"
        }
      },
      "negative_boost": 0.5
    }
  }
}
```

2. Reduce the relevance of recipes with bacon:

```json
{
  "query": {
    "boosting": {
      "positive": {
        "match_all": {}
      },
      "negative": {
        "match": {
          "ingredients": "bacon"
        }
      },
      "negative_boost": 0.5
    }
  }
}
```

But what if we want to apply both preferences simultaneously? Since pasta is a preference rather than a requirement, we need to make it optional. We can achieve this by combining the boosting query with the bool query. Although we can only add a single query clause within the bool query, there's nothing stopping us from adding a compound query that contains multiple query clauses, i.e., leaf queries. Here's an example:

```json
{
  "query": {
    "bool": {
      "must": [
        {
          "boosting": {
            "positive": {
              "term

": {
                "ingredients": "pasta"
              }
            },
            "negative": {
              "match": {
                "ingredients": "bacon"
              }
            },
            "negative_boost": 0.5
          }
        }
      ]
    }
  }
}
```

By combining the boosting query with the bool query, pasta is no longer required, but recipes that contain it receive a higher relevance score. The boosting query reduces the relevance score of recipes with bacon, regardless of whether or not they also contain pasta. Thus, we have constructed a query with both "positive" and "negative" preferences.

As you can see, the boosting query is quite powerful, especially when nested within compound queries. It can be as advanced as you need it to be.

That concludes the boosting query. I hope you find it useful. See you in the next lecture!

If you have any questions or need further clarification, feel free to ask!

## Disjunction Max Query (dis_max)

In this lecture, we'll discuss the disjunction max query, also known as dis_max. It is another compound query that contains query clauses, which can be either leaf queries or compound queries themselves. A document matches the dis_max query if at least one of the specified query clauses matches. Let's dive into an example to understand it better:

```json
{
  "query": {
    "dis_max": {
      "queries": [
        {
          "match": {
            "name": "vegetable"
          }
        },
        {
          "match": {
            "tags": "vegetable"
          }
        }
      ]
    }
  }
}
```

In this example, a document matches the dis_max query if it contains the term "vegetable" in either its name or tags field. By default, the best matching query clause is used to calculate the relevance score of a matching document. In other words, the highest relevance score among the matching clauses is assigned to the document. 

For instance, if a document matches the query clause that searches the tags field and yields the highest relevance score, that score will be used for the matching document. Please note that the document and relevance scores used in this example are fictional.

If only one query clause matches, the relevance score of that clause will be used. This behavior is expected.

By default, the dis_max query works as described above. However, we can also provide a "tie breaker," which rewards documents that match multiple query clauses. This concept is similar to what we discussed earlier in the context of the multi_match query. Here's a quick recap:

Suppose a document matches both query clauses, as was the case in our previous example. By adding the "tie_breaker" parameter to the dis_max query, we can control how much the relevance scores should be boosted. The "tie_breaker" parameter accepts a floating-point number between 0.0 and 1.0. Its default value is 0.0, which results in the default behavior we saw earlier.

Let's take the same document as before and examine the impact of the tie_breaker parameter on the relevance scores. First, Elasticsearch finds the highest relevance score among the matching query clauses. In our example, that score is 5.62. If there are other matching query clauses, their relevance scores are multiplied by the tie breaker value, which is 0.3 in this case. The resulting numbers are then added to the highest relevance score. This process is repeated for any additional matching query clauses. The resulting number is used as the relevance score for the document.

This approach means that the relevance scores of documents are increased for every query clause they match. This behavior is similar to the "should" occurrence type in the bool query, although the calculation method differs.

The dis_max query provides us with control over how much the relevance scores should be boosted. 

By now, this should all sound familiar because it relates to the multi_match query we discussed earlier. Remember the diagram illustrating how the multi_match query with default parameter values is translated into two match queries? That was a simplification. In reality, the match queries need to be wrapped within a compound query because only one "root query" can be executed at a time.

The actual translation involves wrapping these match queries within a dis_max query, as shown here:

```json
{
  "query": {
    "dis_max": {
      "queries": [
        {
          "match": {
            "field1": "value1"
          }
        },
        {
          "match": {
            "field2": "value2"
          }
        },
        ...
      ],
      "tie_breaker": 0.3
    }
  }
}
```

Please note that the translation of the multi_match query depends on the specific parameters provided. The example above demonstrates the translation when the "type" parameter is set to "best_fields," which is the default value. The multi_match query does not perform any magic; it's a convenience query that simplifies the writing of queries and acts as an abstraction layer.

That covers the dis_max query. It is a useful query when you have multiple query clauses that don't necessarily need to match. You can let Elasticsearch assign the highest relevance score to each document by default or give a relevance boost for each additional query clause that matches.

I hope this clarifies the dis_max query for you. See you in the next lecture!

If you have any questions or need further clarification, feel free to ask!

## Nested Data Type and Query

In this lecture, we'll discuss the nested data type and how it enables us to query objects independently within Elasticsearch. To understand this concept better, let's work with a different data set. I have prepared a cURL request for the Bulk API in advance, which you can find in the GitHub repository if you'd like to follow along. 

To give you an idea of the type of documents we'll be working with, here's an example document representing a food recipe:

```json
{
  "name": "Spaghetti Carbonara",
  "tags": ["pasta", "italian"],
  "ingredients": [
    {
      "name": "spaghetti",
      "amount": 200,
      "unit": "grams"
    },
    {
      "name": "parmesan",
      "amount": 60,
      "unit": "grams"
    },
    ...
  ],
  ...
}
```

Each document represents a food recipe, with fields such as name, tags, and ingredients. We'll focus on the ingredients field for this lecture. It is an array of objects, where each object represents an ingredient. The ingredient object contains a name, amount, and unit. Both the amount and unit fields are optional and may not exist for all ingredients.

Let's move to Kibana and query the data. I have prepared a bool query in advance. Our goal is to find recipes containing parmesan with an amount of at least 100. The query is straightforward, so let's run it.

The query returns six recipes that match our criteria. However, upon inspection, we find that some of the matches don't seem to satisfy our requirements. For example, the first ingredient doesn't have an amount or unit, and the second one has an amount of only 60, which is below our required 100. This leads to the question of why these recipes are included in the results.

To answer this question, let's examine the mapping. Since we didn't add explicit field mappings before importing our test data, Elasticsearch generated dynamic field mappings for us automatically. If we inspect the ingredients field, we can see that it was mapped as an object field. This can be inferred from the presence of the "nested properties" key, which implicitly specifies the object data type. Therefore, the field is mapped as the object data type, and we are essentially dealing with an array of objects in this case.

Earlier in the course, we discussed the behavior of arrays of objects, so let's quickly recap. Internally, the values for each object key are grouped together and indexed as an array. When we query a field, Elasticsearch searches through all of the values. This is the reason behind the unexpected query results we encountered earlier.

To resolve this issue, we need to do two things: map the ingredients field as the nested data type and use a special query designed for nested fields. To achieve this, we need to reindex the documents into an index that contains the updated mapping. The easiest way is to delete the existing recipes index and recreate it with the desired field mappings.

Here's an example of the field mapping for the ingredients field:

```json
{
  "mappings": {
    "properties": {
      "ingredients": {
        "type": "nested"
      },
      ...
    }
  }
}
```

Note that we can leave out the mappings for subfields and let Elasticsearch map them dynamically. The crucial part is setting the "type" parameter to "nested" for the field. This instructs Elasticsearch to index the objects in a way that maintains relationships between object values, allowing us to query them independently. Internally, Elasticsearch indexes each nested object as a separate hidden document, which is a Lucene document. This is why we need to query them in a specific way.

Now that the new mapping is in place, let's index the recipes again using the updated mapping. Once indexing is complete, we can return to Kibana.

Before we demonstrate how to query nested fields, it's worth noting that we cannot query fields of the nested data type using regular queries. While we won't receive any errors when attempting to query them, it's still preferable to not receive confusing and potentially misleading results. Therefore, we must exercise caution when querying arrays of objects, regardless of whether the field is mapped with the nested data type or not.

Now let's see how we can actually query nested fields using a specialized query called the nested query. Here's an example of how to structure a nested query:

```json
{
  "query": {
    "nested": {
      "path": "ingredients",
      "query": {
        "bool": {
          "must": [
            {
              "match": {
                "ingredients.name": "parmesan"
              }
            },
            {
              "range": {
                "ingredients.amount": {
                  "gte": 100
                }
              }
            }
          ]
        }
      }
    }
  }
}
```

In the nested query, we first specify the path to the nested field relative to the root of the document. In this case, the path is just "ingredients." If the field were nested within another field, we could use the dot notation known from field mappings. 

Next, we define the search constraints within the "query" parameter. Within this object, we can add any search query we want to run on the nested objects specified by the path. In this example, we include our existing bool query since everything related to the nested data type is handled automatically.

Note that even though we specified the "ingredients" field as the path, we still need to include it within our query using dot notation (e.g., "ingredients.name" and "ingredients.amount").

With this configuration, let's run the query and see what happens. This time, we only receive a single match, which is what we initially expected. Let's examine the matched recipe's parmesan ingredient and verify that everything looks good.

As you can see, the amount is indeed greater than or equal to 100, satisfying the constraints specified in our query. By using the nested data type and query, we successfully applied multiple constraints to the same nested object, achieving the desired outcome.

It's important to note that even though the nested query defines constraints for the nested objects, the query always returns the root document when there is a match.

Lastly, I briefly want to touch on how the nested query handles relevance scoring, specifically how matching child objects affect the parent document's relevance score. Since each nested object is actually a separate document internally, Elasticsearch calculates a relevance score when the nested objects match a query. The parent document's relevance score calculation can be configured using the "score_mode" parameter. By default, the average relevance score of the matching child objects is used for the parent document. Other options include using the minimum or maximum relevance score or adding all of them together to obtain the sum. Additionally, we can choose to ignore the child objects in terms of relevance scoring by using a value of zero.

There is more to nested objects than what we covered here, so we'll continue exploring them in the next lecture.

If you have any questions or need further clarification, feel free to ask!

## Inner Hits with Nested Query

In the previous lecture, we explored how to map and query arrays of objects independently using the nested query. However, when using the nested query, Elasticsearch only returns the parent document whenever a nested object matches. While this is the general behavior and works well, there might be cases where we want to know which specific nested objects caused the match. This is where inner hits come into play.

Inner hits can be useful for various use cases, including highlighting matches. Let's revisit the query from the previous lecture and see how inner hits work.

Enabling inner hits is straightforward. We just need to add a parameter named "inner_hits" to the nested query. The value for this parameter should be an empty object, at least when using the default behavior. 

Let's run the query and examine the results. At the bottom of the results, we can see the inner hits. Now let's discuss the additional data that has been added. It can be a bit overwhelming at first, so let's break it down step by step.

Here is the overall structure of the search results, with the actual hits omitted:

```json
{
  "took": ...,
  "timed_out": ...,
  "hits": {
    "total": ...,
    "max_score": ...,
    ...
  },
  ...
}
```

Each hit represents a document and includes some metadata. The document itself is available within the "_source" key, which is nothing new.

When we specify the "inner_hits" parameter, a new object is added for the "inner_hits" key, which contains information about the inner hits. This object is added at the same level as the "_source" object, which is the root of each hit.

Within the "inner_hits" object, another object is added for each field that has inner hits. In our example, we searched the nested objects within the "ingredients" field. By default, the key for this object is named the same as the path specified within the nested query.

Within each field's object, we have a "hits" object, which has the same structure as the outermost "hits" object. Let's focus on the "hits" object, which contains the actual inner hits.

These inner hits represent the matching nested objects for the "ingredients" path. The "_nested" key contains information about the matched nested object. The most interesting piece of information is the "offset" key, which defines the nested object's offset within the parent document's "_source" object. This offset can be thought of as the index within an array, starting from zero. 

It's important to note that inner hits are sorted by their relevance scores by default. Therefore, the order in which they appear may differ from the order within the document's "_source" object. The "offset" value tells us where the inner object appears within the "_source" object.

Now, I understand that the JSON object can be overwhelming to look at. However, keep in mind that you will usually interact with search results programmatically, so you won't have to examine the raw JSON frequently.

To make it slightly easier to read, here's the JSON object shown with dot notation:

```json
{
  ...
  "hits.inner_hits.ingredients.hits": {
    ...
  },
  ...
}
```

Even with dot notation, the object can still be complex and overwhelming, but that's the nature of it. 

Now let's briefly cover two simple parameters related to inner hits:

1. The "name" parameter allows us to change the key that appears directly within the "inner_hits" object in the results. By default, it uses the path specified within the nested query. While it's typically not necessary to change it, there might be cases, especially with complex queries containing multiple nested queries, where changing the name can provide clarity or avoid conflicts.

2. The "size" parameter allows us to configure how many inner hits we want to be returned for each matching document. By default, up to three hits are returned, sorted by relevance scores. In our example, we increased this to include the top ten inner hits.

There are a few more parameters related to inner hits, but they are not frequently used, so we won't cover them here.

That's it for inner hits! With the nested query, we can query nested objects independently. However, if we also want to know why a particular object matched the query, we can utilize inner hits. Inner hits provide additional information about the specific nested objects that caused the match.

If you have any questions or need further clarification, feel free to ask!

## Limitations of Nested Fields

Let's conclude our discussion on nested fields by exploring a few limitations that you should be aware of. It's important to note these limitations, although there's no guarantee that you will end up using nested fields in your specific use case. 

1. Performance Considerations: Indexing and querying nested fields can be expensive in terms of performance. Elasticsearch creates an Apache Lucene document for each nested object. For example, if you index a million documents, each containing ten nested objects, you will end up with a total of 11 million documents. However, your index will still show only one million documents since the Lucene documents are hidden and managed internally. This behavior comes with a performance cost. Elasticsearch is generally fast, so unless you're dealing with large amounts of data and high query throughput, you may not notice a significant performance penalty. However, as you scale up your usage, you may experience degraded performance and encounter problems.

To mitigate the risk of performance degradation, Elasticsearch provides a couple of safeguards. Let's briefly look at them:

2. Specialized Queries: Working with nested fields requires the use of specialized queries. However, as you saw earlier, the nested query is highly flexible and allows us to nest any normal query within it. This doesn't necessarily limit us but requires us to write queries in a slightly different way.

3. Limit on Nested Fields: There is a limit on the number of fields with the nested data type that can be added to an index. By default, this limit is set to 50, which is typically sufficient for most use cases. It is unlikely that you will encounter this limit. If, for some reason, you do need to increase this limit, it's important to understand that it may indicate an incorrect mapping of your documents.

4. Maximum Nested Documents: Each document in Elasticsearch can contain a maximum of 10,000 nested documents across all nested fields within that document. This limit is in place to prevent out-of-memory exceptions. While it is possible to increase this limit, it is generally not recommended. It's important to consider this limit when designing your data structure. 

Let's consider an example to illustrate the impact of these limitations. Suppose we are running a service similar to Shopify, where we provide webshops for companies. It may seem logical to store the orders for each webshop within a nested "orders" field. However, if we analyze the performance implications of storing orders in this way within Elasticsearch, it becomes clear that it's not a good design. We have two nested fields: "orders" and "lines" (representing the order lines within each order). The number of objects between these two fields contributes to the 10,000 nested objects limit. It's only a matter of time before a customer reaches 10,000 orders, especially considering that each order contains at least one order line. This design is not scalable.

A better approach would be to split the data into two separate indices: one for webshops and one for orders. This way, the 10,000 nested objects limit only applies to the "lines" field within the orders index. The number of objects within a document does not grow over time because once an order is complete, no new order lines are added. Therefore, no order will ever exceed or come close to the 10,000 nested objects limit. When mapping your documents and deciding to use nested fields, it's crucial to keep this limitation in mind. Consider whether it is realistic for a document to have thousands of nested objects. If it is, you might need to reconsider your document mapping strategy.

By keeping these limitations in mind and designing your document mappings accordingly, you can work effectively with nested fields in Elasticsearch.

If you have any further questions or need additional clarification, feel free to ask!

## Joining Queries in Elasticsearch

In this section, we will explore joining queries, which allow us to query relationships between documents. While we have covered a lot about searching for documents, we will now focus on querying relationships in Elasticsearch.

To begin, let's briefly consider how data can be stored in a relational database such as MySQL or PostgreSQL. Suppose we want to store employees in a database, where each employee is associated with an address. In relational databases, it is best practice to normalize the data by storing it in two different tables and linking them with a foreign key. This normalization approach allows for efficient querying of relationships between different pieces of data, which is the core principle of relational databases.

Similarly, we might want to store information about departments within companies and the cities where they are located. In this case, the database schema could include a table for departments and another for cities, where each department has a foreign key linking it to the city in which it is located. This represents a one-to-many relationship between departments and cities.

Now, why are we discussing relational databases in the context of Elasticsearch? The reason is that most developers are familiar with relational databases, and it's important to understand that storing data in Elasticsearch follows a different approach. In Elasticsearch, denormalizing the data is generally recommended for optimal performance. This means that instead of splitting the data into separate tables and using foreign keys, you store the data in a denormalized form. This approach is similar to how data is stored in NoSQL databases like MongoDB, where joins are either avoided altogether or handled at the application level.

You might wonder if denormalizing the data is inefficient and leads to wasted disk space. While it's true that denormalization may result in redundant data storage (e.g., storing the city name for each department), it's important to note that Elasticsearch is not typically used as a primary data store. By not treating Elasticsearch as the primary data store, we gain the flexibility to store data in ways that are optimized for quick data retrieval. Therefore, sacrificing disk space to increase the performance and throughput of the Elasticsearch cluster can be an acceptable trade-off.

It's worth mentioning that Elasticsearch does not support joins in the same way as relational databases. However, it does offer some simple ways of joining documents. It's important to note that these join-like queries in Elasticsearch can be less efficient compared to relational databases, especially when dealing with a large number of documents. Keep this in mind when working with joining queries and consider the performance implications.

In the upcoming lectures, we will explore the tools and techniques available in Elasticsearch for mapping and querying document relationships. Elasticsearch provides specific functionalities to handle relationships between documents effectively.

If you have any further questions or need additional clarification, feel free to ask!

## Defining Document Relationships in Elasticsearch

The first step in defining document relationships in Elasticsearch is to incorporate them into the mapping. Elasticsearch provides a special type of field called a "join field" for joining documents and defining relationships within the document hierarchy.

Let's start by adding the mapping for the join field. The join field can be named anything, similar to other fields. For demonstration purposes, let's name it "join_field". We'll define it as an object field, which is achieved by assigning the value of "object" to the field.

```json
"join_field": {
  "type": "object"
}
```

To specify that this field represents a join relationship, we need to set its data type to "join". This special data type is dedicated to defining document relationships.

```json
"join_field": {
  "type": "join"
}
```

Next, we need to define the possible relations between different types of documents within the document hierarchy. This is done using the "relations" object within the join field.

```json
"join_field": {
  "type": "join",
  "relations": {}
}
```

Within the "relations" object, we define key-value pairs that represent the relationships between documents. Let's continue with the example from the previous lecture and add a relationship between a "department" and an "employee".

```json
"join_field": {
  "type": "join",
  "relations": {
    "department": "employee"
  }
}
```

In this example, "department" is the key representing the parent document type, and "employee" is the value representing the child document type. The names "department" and "employee" are arbitrary and can be chosen as per your preference. It's important to note that the key does not need to match the name of the index.

By defining this relationship, we have effectively established a parent-child relationship between the "department" and "employee" document types. This enables us to leverage this relationship when adding documents and querying the data based on these relationships.

If we wanted to define multiple child types for the same parent, we could change the value from a single string to an array of strings. Each string within the array would represent a child document type associated with the parent.

Now that we have defined the document relationship, let's proceed by adding some sample documents to the index to have data for working with in subsequent lectures.

If you have any further questions or need additional clarification, feel free to ask!

## Adding Documents and Defining Document Relations

Now that we have the mapping in place, let's proceed to add some documents to the index. When working with document relationships, the process of adding documents is slightly different than usual.

Let's start by adding two departments to the index using the following queries:

```json
PUT department/_doc/1
{
  "name": "Department 1"
}

PUT department/_doc/2
{
  "name": "Department 2"
}
```

Note that when adding documents related to a parent document, we need to specify which relation the document belongs to. In this case, since we are adding departments, we need to specify the relation named "departments" (which is the key of the join field defined in the mapping).

To do this, we add a key that matches the name of the join field ("join_field" in our example) and set the value to "department". This indicates that the document is a department.

```json
PUT department/_doc/1
{
  "name": "Department 1",
  "join_field": "department"
}

PUT department/_doc/2
{
  "name": "Department 2",
  "join_field": "department"
}
```

Next, let's add some employees to the index. For each employee, we need to specify the parent document to which the employee belongs (i.e., the department). This is done by adding an object as the value for the join field.

```json
PUT department/_doc/3
{
  "name": "Employee 1",
  "join_field": {
    "name": "employee",
    "parent": "1"
  }
}
```

In this example, we are adding an employee document ("Employee 1") to the department with an ID of "1". We specify the relation name as "employee" and set the parent option to "1" to associate the employee with the department.

However, when adding child documents, such as employees, we encounter an error related to the join field and routing. Routing is a mechanism used by Elasticsearch to determine the shard where a document is stored.

To resolve this issue, we need to include a query parameter named "routing" with a value that matches the ID of the parent document. This ensures that the parent and child documents are stored on the same shard.

```json
PUT department/_doc/3?routing=1
{
  "name": "Employee 1",
  "join_field": {
    "name": "employee",
    "parent": "1"
  }
}
```

After adding the routing query parameter, the document can be successfully added, and the department and employee are stored on the same shard.

To add more employees to the index, you can repeat the process by specifying the parent department and adjusting the routing query parameter accordingly. For example:

```json
PUT department/_doc/4?routing=2
{
  "name": "Employee 2",
  "join_field": {
    "name": "employee",
    "parent": "2"
  }
}
```

By following this approach, you can add as many departments and employees as needed, establishing the desired document relationships.

If you have any further questions or need additional clarification, feel free to ask!

## Querying Document Relations

Now let's write our first query in the context of document relations. We'll start with a simple query named "parent_id," which retrieves the child documents based on the ID of the parent documents.

In our case, we can use this query to retrieve the employees for a given department.

Let's add the query object:

```json
{
  "query": {
    "parent_id": {}
  }
}
```

To specify the relation we want to query, we need to include the `type` option, which corresponds to the child relation type we want to retrieve. In this case, we set the value to "employee" since we want to retrieve employee documents.

```json
{
  "query": {
    "parent_id": {
      "type": "employee"
    }
  }
}
```

To specify the ID of the parent document (department), we use the `id` option. Let's choose the first department (ID: 1) as an example:

```json
{
  "query": {
    "parent_id": {
      "type": "employee",
      "id": "1"
    }
  }
}
```

Now let's run the query and see if we get the expected results. The query should match the employees associated with the specified department.

Within the search results, we can see that the query matches the documents, which is what we expected based on our test data.

If we change the parent ID to "2," the query should match the employees in the other department. Let's try that:

```json
{
  "query": {
    "parent_id": {
      "type": "employee",
      "id": "2"
    }
  }
}
```

Indeed, we can now see the employees from the other department in the search results.

That's all there is to this query. As promised, it's quite straightforward.

Before ending the lecture, I'd like to mention two things about the search results:

1. Notice how the hits contain the join field within the `_source` key. In this case, we already know the values at query time, so it might not be relevant to us. However, in other queries, it can be useful to check the types of the matching documents.

2. Additionally, notice how the hits include a `_routing` key with a value of "2." This number matches the ID of the parent document (department). Remember that a parent document and all of its child documents must be placed on the same shard, as mentioned in the previous lecture. The `_routing` key indicates that Elasticsearch uses the ID of the parent document to determine the shard on which the documents are stored. This is the default behavior and can be overridden by using the `routing` query parameter. However, custom routing is not commonly used.

If all of this went over your head, don't worry! It's just some background knowledge that's not essential to understand when using the "parent_id" query.

If you have any further questions or need additional clarification, feel free to ask!

## Querying Child Documents Based on Parent Document Criteria

In some cases, retrieving child documents based on the ID of their parent document might not be sufficient. You might not know the parent document's ID, or you might want to add additional conditions other than the document ID. This can be accomplished with a query named "has_parent."

The "has_parent" query allows you to define a query that the parent document should match for a child document to be returned. In other words, the query returns the child documents where the parent document matches certain criteria.

Let's see how it works. First, let's add the name of the query, "has_parent," and an empty object as the value:

```json
{
  "query": {
    "has_parent": {}
  }
}
```

Within this object, the first thing we need to do is specify the parent relation name using an option named "parent_type." Since we'll be adding conditions to departments, the relation name will be "department":

```json
{
  "query": {
    "has_parent": {
      "parent_type": "department"
    }
  }
}
```

Next, we need to specify the conditions that the parent document must satisfy. We do this within an option named "query," where we can specify any query that we have seen before. In this example, let's use a term query to match the development department by its name:

```json
{
  "query": {
    "has_parent": {
      "parent_type": "department",
      "query": {
        "term": {
          "name.keyword": "development"
        }
      }
    }
  }
}
```

Now let's run the query and see what happens. Looking at the results, we can see that the matching documents belong to a parent with an ID of 1, which corresponds to the development department.

You can add any complexity to the query if you want, such as using a bool query.

So far, we have successfully retrieved the employees for the development department. However, the "has_parent" query can do more than that.

One feature worth mentioning is the support for relevance scoring. By default, the query ignores the relevance score from the matching parent document. This means that how well the parent document matches has no effect on the relevance scores of the child documents. The default behavior is that a flat score of 1 is added to the score of each matching child document.

To change this behavior and take the relevance score of the matching parent document into account, we can set the "score" option to true:

```json
{
  "query": {
    "has_parent": {
      "parent_type": "department",
      "query": {
        "term": {
          "name.keyword": "development"
        }
      },
      "score": true
    }
  }
}
```

Before running the query, let's look at the results from the previous query. Notice how all the matches have a relevance score of 1. This is the default behavior where a flat score of 1 is applied to the matching documents from the matching parent document.

Now, let's run the modified query and observe the difference. Notice how the relevance scores have now increased by approximately a third. This increase is because the relevance score of the matching parent document is now taken into account, and it is reflected in the scores for the child documents. In other words, the relevance scores for the matches of the term query are used as the relevance scores for the child documents.

It's important to note that this feature is most useful when the query is not searching for an exact value. In our example, we used an exact match, so the relevance scoring doesn't show its full potential. However, in scenarios where a query like the match query is used to search a text field, the relevance scores of the matching parent documents would likely differ significantly based on how well they match the query. By setting the "score" option to true, we ensure that the child documents belonging to the best matching parent document are scored the highest within the results.

Although our query is not the best example to showcase this feature, I hope you understand the concept of applying the relevance score to child documents. If you need more control over how the child documents are sorted, you can use the "function_score" query, which we'll cover later in the course. However, it's not a very common practice.

If you do need this behavior and want to explore it further, I have attached a link to an example that demonstrates how it can be done.

That's it! As you can see, the "has_parent" query offers more flexibility than the "parent_id" query in cases where you don't know the ID of the parent document or when you're looking for more than a single parent document.

If you have any further questions or need additional clarification, feel free to ask!

## Querying Parent Documents Based on Child Document Criteria

Now that you've learned how to retrieve child documents based on parent document criteria, let's explore the opposite scenario: retrieving parent documents based on criteria placed on their child documents. The query that enables us to do this is named "has_child."

Let's see it in action. First, let's add an empty object for the "has_child" key:

```json
{
  "query": {
    "has_child": {}
  }
}
```

Within this object, the first thing we need to do is define the relation type of the child documents using the option named "type." In this example, the value will be "employee":

```json
{
  "query": {
    "has_child": {
      "type": "employee"
    }
  }
}
```

Next, let's add an empty query object. This is where we'll define the constraints for the child documents (i.e., the employees):

```json
{
  "query": {
    "has_child": {
      "type": "employee",
      "query": {}
    }
  }
}
```

Now, let's define the constraints for the child documents. In this example, we want to match employees with an age greater than or equal to 50 and boost the relevance score if they are male. We can achieve this by using a bool query:

```json
{
  "query": {
    "has_child": {
      "type": "employee",
      "query": {
        "bool": {
          "must": [
            {
              "range": {
                "age": {
                  "gte": 50
                }
              }
            },
            {
              "term": {
                "gender.keyword": "male"
              }
            }
          ]
        }
      }
    }
  }
}
```

Now, let's run the query and see the results. Looking at the results, we can see that the development department matches because it has an employee with an age of 52.

If we change the age constraint to 60, we will no longer get a match for the department. Let's try that:

```json
{
  "query": {
    "has_child": {
      "type": "employee",
      "query": {
        "bool": {
          "must": [
            {
              "range": {
                "age": {
                  "gte": 60
                }
              }
            },
            {
              "term": {
                "gender.keyword": "male"
              }
            }
          ]
        }
      }
    }
  }
}
```

This time, the department no longer matches the criteria.

To recap, with the "has_child" query, we can match parent documents that contain child documents matching certain criteria. This criteria can be any query that you have learned so far, providing maximum flexibility.

There are two more things worth mentioning about the "has_child" query. First, like the "has_parent" query, we can include the relevance scores of matching child documents. However, the option for this is named "score" with a "score_mode." There are five score modes available:

- "min" and "max" modes take the lowest and highest score, respectively, of any matching child document and map it into the relevance score for the parent document.
- "sum" and "avg" modes include all child documents' relevance scores and calculate the sum and average, respectively. The resulting number is then aggregated into the relevance score of the parent documents.
- The "none" mode doesn't consider the relevance scores of child documents at all. This is the default behavior, so you can either set the value to "none" explicitly or simply leave it out.

To demonstrate the score mode, let's add the "score" and "score_mode" options to our query. For example, let's set the mode to "sum":

```json
{
  "query": {
    "has_child": {
      "type": "employee",
      "query": {
        "bool": {
          "must": [
            {
              "range": {
                "age": {
                  "gte": 50
                }
              }
            },
            {
              "term": {
                "gender.keyword": "male"
              }
            }
          ]
        }
      },
      "score": true,
      "score_mode": "sum"
    }
  }
}
```

Now, let's run the query. Notice how the relevance score of the matching document is no longer just 1. The score has increased by approximately a third because the sum of the matching child documents' scores has been aggregated into the score. This approach is useful when you want to find parent documents that not only have child documents matching the criteria but also want to take into account how well the child documents match. The number of matching child documents may also affect the relevance score when using the "sum" scoring mode.

The second point to mention is that the "has_child" query allows you to specify the minimum and maximum number of children that must match for the parent document to be included in the search results. This can be achieved by adding the "min_children" and "max_children" options. For example, let's set the minimum number of children to 2 and the maximum to 5:

```json
{
  "query": {
    "has_child": {
      "type": "employee",
      "query": {
        "bool": {
          "must": [
            {
              "range": {
                "age": {
                  "gte": 50
                }
              }
            },
            {
              "term": {
                "gender.keyword": "male"
              }
            }
          ]
        }
      },
      "min_children": 2,
      "max_children": 5
    }
  }
}
```

When we run the query, we no longer get any matches. That's because we set the minimum number of children to 2, but the department that matched before only has one child document that matches the specified criteria. You can specify either one or both of these options based on your requirements.

Lastly, it's worth mentioning that the "has_child" query also supports sorting parent documents by child documents in the same way the "has_parent" query supports sorting. However, this requires scripting, and since we haven't covered scripting yet, I'll attach a link to an example for reference.

That's it for this lecture! If you have any further questions or need additional clarification, feel free to ask!

## Querying Multi-level Relations

So far, we have been working with single-level relations, but it's also possible to have multi-level or nested relations. In the context of our example, we could have a company containing departments, which in turn have employees. To demonstrate this, I will create a new index named "company" that includes these relations, along with a "supplier" relation that belongs to a company. This will show an example of one relation containing multiple relation types.

Let's start by creating the index and mapping. Most of the query is prepared in advance, so we just need to populate the relations object, which is the interesting part. First, we need to define the "company" relation type, which will contain both the "department" and "supplier" relation types. We do this by setting the value as an array of strings:

```json
{
  "mappings": {
    "properties": {
      "relations": {
        "type": "join",
        "relations": {
          "company": ["department", "supplier"]
        }
      },
      "department": {
        "type": "join",
        "relations": {
          "company": "employee"
        }
      }
    }
  }
}
```

In the example above, the "company" relation type is the parent relation for both the "department" and "supplier" relations. This means a company can have multiple departments and suppliers. Next, we define that a company can have multiple employees, which adds another level of relations. We do this by specifying the name of the existing relation type ("department") as the key within the "relations" object and defining the child relation type ("employee") in the same way as before.

Now, let's index some documents to the new relation. We have prepared queries to add a company and a department, which are similar to the queries you've seen before. Let's run these queries to add the company and department.

Now that we have indexed the documents in the context of multi-level relations, let's discuss how to search for them. The answer is quite simple: you do it in the same way as before, using the queries you've already learned. The "has_parent," "has_child," and "parent_id" queries work the same way in the context of multi-level relations because they operate on the relation between two types. The queries are not concerned with where the types are placed in the hierarchy; they work in the same way.

However, if you want to restrict the matching documents on multiple relation levels, you may need to nest the queries. For example, let's say we want to retrieve companies that have at least one department containing an employee named "John Doe." Since the employee type is a grandchild of the company type, we need to nest the queries. Let's build that query:

```json
{
  "query": {
    "has_child": {
      "type": "department",
      "query": {
        "has_child": {
          "type": "employee",
          "query": {
            "term": {
              "name.keyword": "John Doe"
            }
          }
        }
      }
    }
  }
}
```

In the query above, we use the "has_child" query for the "department" type to find companies that have departments matching the given query (in this case, another "has_child" query). The nested "has_child" query finds employees with the name "John Doe." If the innermost query returns at least one matching document (i.e., employee), the department is included in the outermost query, causing the company to be included in the results.

Let's run the query and check the results. As we can see, only the company that contains a department with an employee named "John Doe" is matched. If we change the name or use a bogus name, the company will no longer be matched.

That's it! You now know how to define and query multi-level relations. You can use the queries you've learned in different combinations depending on the data you're working with and the data you want to retrieve.

If you have any further questions or need additional clarification, feel free to ask!

## Returning Inner Hits for Queries on Join Fields

In an earlier section, you learned about using nested inner hits to see which nested objects caused a document to match. However, inner hits can also be used for join fields.

Let's explore this concept in this lecture. The process is exactly the same as before, but the inner hits that are returned depend on the query used.

Let's start by returning inner hits for the `has_child` query that you saw in a previous lecture. The query is already provided, so we just need to add the `inner_hits` option to it and run it.

```json
{
  "query": {
    "has_child": {
      "type": "departments",
      "query": {
        "match_all": {}
      },
      "inner_hits": {}
    }
  }
}
```

In the query above, we added the `inner_hits` option with an empty object as the value. This enables us to see the inner hits, which in this case, are the departments that have employees matching the defined query. We can now observe which employees caused each department to match the query.

Let's run the query and see the results. For this particular query, an employee named Daniel Harris matched the specified query, resulting in the `has_child` query matching the "development" department.

The same approach can be applied to the `has_parent` query. Let's see it in action:

```json
{
  "query": {
    "has_parent": {
      "parent_type": "departments",
      "query": {
        "match_all": {}
      },
      "inner_hits": {}
    }
  }
}
```

In the query above, we added the `inner_hits` option to the `has_parent` query. This query matches child documents that have a parent document matching the defined query. By including inner hits, we can now see which department caused each employee to match. In the results, we can determine which parent document influenced the inclusion of a given child document.

Let's run the query and check the results. We can see which department caused each employee to be returned. In this case, it's unsurprisingly the "development" department. In a real-world scenario, the query may match multiple departments, but the concept remains the same.

That's all there is to returning inner hits for queries that use join fields. It allows us to gain insights into the relationships between parent and child documents and understand how the matching process unfolds.

If you have any further questions or need additional clarification, feel free to ask!

## Using Terms Query with Terms Lookup Mechanism

In this section, we will revisit a query you've seen before, the terms query. However, this time we will explore how it relates to join fields.

The basic usage of the terms query is to look up documents that contain one or more specified terms. However, there are cases where including a large number of terms in the query definition becomes impractical. For instance, if you need to include 500 terms, the query would become cumbersome and unwieldy.

To address this issue, the terms query supports something called a "terms lookup" mechanism. In Elasticsearch jargon, this mechanism allows fetching the terms from another document.

Let's dive right in and examine some examples. I have prepared test data in advance and have already run the queries. You can find them in the GitHub repository if you're following along.

The query involves creating two indices: "users" and "stories." Each user has a field named "following," which contains the IDs of the users they are following. Think of this as following someone on Instagram, Snapchat, Twitter, or Facebook.

The goal is to display the stories for a given user, which corresponds to the stories published by the users they are following. To achieve this, we need to search for stories published by the user IDs that the user is following.

Below is the first part of the term query:

```json
{
  "query": {
    "terms": {
      "user": {
        "index": "users",
        "type": "_doc",
        "id": "1",
        "path": "following"
      }
    }
  }
}
```

In the query above, we specify the index and type as "users" and "_doc" respectively. We want to retrieve the user IDs from a specific document, identified by the ID "1." The "path" parameter indicates the field where the user IDs are stored, which is "following" in this case.

Let's run the query and examine the results. We can see that two stories were matched, corresponding to the stories from users with IDs "2" and "3." This is as expected since the user with ID "1" follows these two users.

Now, let's understand what happened behind the scenes. When the coordinating node received the search request, it determined that it needed to retrieve the terms to fulfill the terms query based on the options specified.

Consequently, it sent a request to fetch the document with the specified ID and extracted the values from the "following" field. These values were then used in the terms query. Essentially, this process is equivalent to looking up the user by ID at the application level and using the retrieved values for the terms query.

However, there are significant advantages to letting Elasticsearch handle this internally. If we were to perform the same operation at the application level, we would be making two queries to the Elasticsearch cluster instead of one. The time it takes for Elasticsearch to process a query is relatively short. The difference lies in the time taken to send queries over the network. Although Elasticsearch clusters are usually geographically close to the application server, there is still some network latency to consider. Additionally, the amount of data transferred over the network can impact performance. Suppose a user is following thousands of other users; transferring this data over the network would be inefficient, especially if the IDs are not simple integers but larger values like UUIDs.

By leveraging Elasticsearch's internal mechanism, we achieve better performance. The performance gain depends on the data mapping and volume. It's important to note that the query's performance gradually degrades as the number of terms increases. Elasticsearch requires memory and processing power for each term. There is a limit of around 65,000 terms, which can be configured on a per-index basis. Be mindful of this limit if you anticipate queries that handle a large number of terms.

In summary, this lecture demonstrated how to use the terms query with the terms lookup mechanism to retrieve terms from another document, potentially from another index, and use those terms within the same terms query. Additionally, we discussed how this approach improves performance compared to executing two separate queries.

If you have any further questions or need additional clarification, feel free to ask!

Certainly! Here's the revised text with detailed explanations:

## Limitations and Performance of Join Fields

In this section, we'll discuss a few limitations that apply to join fields and explore the performance aspects of joining queries.

Let's start with the limitations:

1. **Joining Documents in the Same Index:** As mentioned in a previous lecture, documents that we want to join must be stored within the same index. This means that we cannot have departments stored in one index and employees in another index and then attempt to join them together. This limitation exists for performance reasons, as joins would be significantly slower across different indexes.

2. **Parent and Child Documents on the Same Shard:** Another limitation is that parent and child documents must be indexed on the same shard. This requirement was evident when we added documents, as we had to explicitly provide a "routing" parameter to ensure that the documents were assigned to the same shard. This constraint is essential for efficient join operations and maintaining the integrity of the relationships.

3. **One Join Field per Index:** Each index can have only one join field. However, this limitation is not overly restrictive because we can map as many document relationships as needed within that join field. We can also add new relations to an existing join field without any issues.

4. **One Parent per Document:** A document can have only one parent. For example, an employee can belong to only one department. However, a document can have multiple children, enabling a department to have multiple employees, as you have already seen in previous lectures.

Now, let's shift our focus to the performance of joining queries:

Joining queries in Elasticsearch are designed to be efficient and performant. By leveraging the underlying data structures and algorithms, Elasticsearch can execute join operations with high speed and scalability. Join fields are specifically optimized for these types of queries.

To achieve optimal performance, Elasticsearch utilizes the concept of document routing. By assigning documents with the same parent-child relationship to the same shard, Elasticsearch ensures that join operations can be performed locally on a shard without the need for extensive inter-shard communication. This reduces latency and improves query response times.

Additionally, Elasticsearch employs various caching mechanisms to enhance join query performance. The query cache and field data cache are examples of caching mechanisms that can be leveraged to speed up join queries by caching intermediate results and frequently accessed data.

It's important to note that the performance of joining queries can be affected by factors such as the size and complexity of the data, the number of shards in the cluster, the available system resources, and the query workload. Properly configuring and optimizing these aspects can contribute to improved join query performance.

In summary, join queries in Elasticsearch are designed to provide efficient and performant document relationship lookups. By adhering to the limitations of join fields and leveraging Elasticsearch's indexing and caching mechanisms, we can achieve fast and scalable join operations within the same index.

If you have any further questions or need additional clarification, feel free to ask!

## Performance and Considerations of Join Fields

In this section, we'll discuss the performance implications of join fields and the considerations to keep in mind when using them.

To summarize, join queries using the "join" field, specifically parent/child joins, are generally expensive in terms of performance and should be used with caution. It's important to understand the impact of join fields, especially when dealing with large amounts of data.

Join fields introduce additional complexity and overhead, which can lead to slower query performance as the number of documents and relationships increase within an index. The "has_child" and "has_parent" queries, for example, experience degraded performance as the number of child documents pointing to unique parent documents or the number of parent documents themselves increases.

Furthermore, using multi-level relations adds additional overhead to queries, and it is generally advised to avoid this unless necessary.

However, there are scenarios where using a join field can still yield good performance. One such scenario is when there is a one-to-many relationship between two document types, and one type significantly outweighs the other in terms of document count. For instance, if you have recipes as parent documents and ingredients as child documents, and there are significantly more ingredients than recipes, using a join field can be a suitable option. Alternatively, you could also map the ingredients as nested objects, depending on your specific requirements.

It's important to address the question of why we discussed join fields extensively, despite their performance implications and general discouragement. The reason is that there are still valid use cases for parent/child relationships, such as the example mentioned earlier. Additionally, if you have a limited number of documents and do not anticipate significant changes, the performance impact may be acceptable. Ultimately, as the creator of your Elasticsearch mapping, it is essential to provide you with the necessary tools and knowledge to make informed decisions based on your unique use case.

Now, let's address the question of mapping document relationships properly. In Elasticsearch, unlike a relational database, it is generally recommended not to map document relationships explicitly. Elasticsearch excels at efficiently searching through vast amounts of data, and it is optimized for searching rather than traditional relationship mapping.

Instead of trying to map document relationships, a common approach is to denormalize the data. For example, when mapping employees as documents, you can include their address as a regular field within the employee document or as a nested object, depending on your specific needs. The key is to optimize the data structure for efficient searching rather than focusing on explicit relationships.

In summary, while join fields can have performance implications and should be used with caution, it is generally advised to denormalize your data and structure it in a way that maximizes search efficiency. Reserve the use of join fields for cases where denormalization is not suitable, and be aware of the limitations and consequences associated with using join fields.

If you have any further questions or need additional clarification, feel free to ask!