
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