# Retrieving Current Document

To observe the current state of a document, let's retrieve the document with the ID of 100.

```bash
GET /my-index/_doc/100
```

The retrieved document will contain the previously indexed fields, including the modified "in_stock" field and the newly added "tags" field.

```json
{
  "_index": "my-index",
  "_type": "_doc",
  "_id": "100",
  "_version": 2,
  "_seq_no": 1,
  "_primary_term": 1,
  "found": true,
  "_source": {
    "name": "Product",
    "price": 10,
    "in_stock": 4,
    "tags": ["tag1", "tag2"]
  }
}
```

## Replacing the Document

To replace the document, let's modify the "price" field and update the entire document using the same query.

```bash
PUT /my-index/_doc/100
{
  "name": "Replaced Product",
  "price": 15,
  "in_stock": 5
}
```

## Retrieving the Replaced Document

After executing the query, let's retrieve the replaced document to confirm the changes.

```bash
GET /my-index/_doc/100
```

The retrieved document will now contain only the fields that were specified in the replace query. Consequently, the "tags" field, which was not included in the replace query, is no longer present because the entire document was replaced.

```json
{
  "_index": "my-index",
  "_type": "_doc",
  "_id": "100",
  "_version": 3,
  "_seq_no": 2,
  "_primary_term": 1,
  "found": true,
  "_source": {
    "name": "Replaced Product",
    "price": 15,
    "in_stock": 5
  }
}
```

This demonstrates how easy it is to replace documents in Elasticsearch.

> Please note that the examples provided assume the existence of an index named "my-index" and the use of the default document type "_doc".

## Deleting Documents

We have covered quite a few ways of managing documents so far, and the last one we have yet to cover is deleting documents.

As you might have guessed, deleting documents is also super easy.

In fact, it's quite intuitive, especially considering the REST API.

To delete a document, we use the same query structure that we used to retrieve a document, but with a change in the HTTP verb to "DELETE."

```bash
DELETE /my-index/_doc/100
```

Executing this query will remove the document from the index.

After running the query, the document will be deleted, and any subsequent attempt to retrieve it will result in a "not found" response.

```json
{
  "found": false,
  "_index": "my-index",
  "_type": "_doc",
  "_id": "100",
  "_version": 4
}
```

It is worth noting that, similar to updating documents, you can also delete documents based on a query condition. We will explore this further in upcoming sections.

> Please note that the examples provided assume the existence of an index named "my-index" and the use of the default document type "_doc".

## Understanding Routing in Elasticsearch

We have now covered indexing, updating, deleting, and retrieving documents, and it all seemed quite straightforward, didn't it? But have you ever wondered how Elasticsearch knows which shard to store a document on, or which shard to search for when retrieving or updating a document? The answer lies in routing.

Routing, in its basic form, refers to the process of determining the shard of a document. It is used not only when indexing a document but also when searching, updating, or deleting a specific document.

When we index a new document, Elasticsearch uses a simple formula to calculate the shard where the document should be stored. The formula is based on the document's ID, which by default is used as the routing value.

The same routing formula is used when retrieving, updating, or deleting documents. By specifying the ID, Elasticsearch can determine the shard on which the document resides.

It's important to note that searching for documents based on criteria other than their IDs works differently and will be covered in later sections.

Routing is handled transparently by Elasticsearch, making it easier for us as users. By providing a default routing strategy, Elasticsearch ensures documents are allocated to the appropriate shards and distributed evenly across the index.

It's worth mentioning that the default routing strategy can be changed, but we won't delve into that topic right now. We'll cover it in more detail later in the course.

In addition to routing, Elasticsearch stores metadata alongside indexed documents. When retrieving a document, you saw that the original JSON object is stored in the `_source` field. The document's identifier is stored in the `_id` field. Another meta field, `_routing`, was mentioned in the routing formula. However, you won't see the `_routing` field in the query results unless you specify a custom routing value during document indexing.

Before concluding this lecture, here's an interesting tidbit: Have you ever wondered why the number of shards cannot be changed once an index is created? The answer lies in the routing formula itself. The number of shards is used in the formula, so changing the number of shards would yield different results. This poses a challenge for existing documents. If the number of shards is increased, Elasticsearch may fail to locate documents based on their IDs, resulting in empty responses. Additionally, adding shards could lead to uneven distribution of documents across shards.

To modify the number of shards, you need to create a new index and reindex the documents into it. Elasticsearch provides the Shrink and Split APIs to facilitate this process.

That's a little bonus information about routing and shard allocation in Elasticsearch.


> Please note that the examples provided assume a basic understanding of Elasticsearch and its terminology.

## Understanding Reading Data in Elasticsearch

In this lecture, we will delve into the details of how Elasticsearch reads data. Please note that we will focus on reading a single document, not search queries, which we will cover later in the course.

When a read request is made, it is received by a specific node in the Elasticsearch cluster. This node is referred to as the coordinating node and is responsible for coordinating the request.

The coordination process begins by determining the location of the requested document. This is achieved through routing, as discussed earlier. Routing resolves to the primary shard (or a replication group) where the document is stored. In most cases, the document is replicated across shards for redundancy and high availability.

Instead of directly retrieving the document from the primary shard, Elasticsearch employs Adaptive Replica Selection (ARS). ARS selects the most suitable replica shard copy based on various factors, including performance considerations. The details of ARS will be covered in more depth later in the course.

Once a replica shard is chosen, the coordinating node forwards the read request to that shard. The shard responds with the requested document.

The coordinating node collects the response from the shard and sends it back to the client. The client can be an application using one of the Elasticsearch SDKs, Kibana, or even the command-line interface of your development machine.

Now that we have explored the reading process in Elasticsearch, let's move on to understanding how writing data works.

## Understanding Writing Data in Elasticsearch

Now that we have covered how Elasticsearch reads data, let's explore how it writes data. 

When data is written to Elasticsearch, it goes through a process called routing. This process determines where the data should be stored within the system. During routing, Elasticsearch uses a formula to calculate which shard (a smaller unit of data storage) the document should be assigned to. By default, Elasticsearch uses the document's ID for routing.

When a write request is made, Elasticsearch first determines the replication group responsible for storing the data. The request is then routed to the primary shard within that replication group. The primary shard is the primary responsible for handling write operations.

The primary shard performs several tasks. It validates the write request, ensuring that the request is structurally correct and that the field values are valid. For example, if an attempt is made to add an object to a numeric field, the validation process will return an error. Once the request passes validation, the primary shard writes the data locally on its own shard.

To ensure data consistency and availability, the primary shard forwards the write operation to replica shards. Replica shards are copies of the primary shard and help distribute the data across the system. The primary shard forwards the operation to its replica shards in parallel to improve performance.

It is important to note that even if the operation cannot be replicated to the replica shards, the write operation will still be considered successful.

To summarize, when writing data to Elasticsearch, the write request is routed to the primary shard responsible for the data. The primary shard validates the request, performs the write operation locally, and then distributes the operation to replica shards, if any.

Now, let's dive a bit deeper into the writing process and discuss how Elasticsearch handles failures related to data replication.

Given that Elasticsearch is a distributed system with asynchronous operations, failures can occur due to various factors, such as hardware failures. These failures can pose challenges, especially if they happen during critical moments.

For example, let's consider a scenario where we are indexing a new document. The primary shard validates the operation and indexes the document on its own shard. In a replication group with replica shards, the primary shard sends the operation to its replicas. However, if the primary shard fails before the operation reaches all the replicas, it can lead to inconsistencies in the data.

To recover from such failures, Elasticsearch initiates a recovery process. During recovery, one of the replica shards is promoted to become the new primary shard, ensuring the replication group always has a primary shard. However, in the example mentioned earlier, the remaining replica shard would have a different state compared to the new primary shard because it did not receive the index operation.

This inconsistency can lead to unpredictable behavior when retrieving the document, as the document may only be found half of the time, depending on which shard serves the retrieval request.

Handling such failures and maintaining data consistency is a crucial aspect of Elasticsearch. To address these challenges, Elasticsearch utilizes mechanisms such as primary terms and sequence numbers.

Primary terms are used to differentiate between old and new primary shards when the primary shard of a replication group changes. Each replication group has a primary term, which acts as a counter to track the number of times the primary shard changes. When a primary shard fails and is replaced by a replica shard, the primary term for that replication group increases.

Sequence numbers are assigned to each write operation. They act as counters that are incremented for each operation processed by the primary shard. These sequence numbers help Elasticsearch track the order of operations on a primary shard.

By utilizing primary terms and sequence numbers, Elasticsearch can recover from situations where the primary shard changes. Instead of comparing data on disk, Elasticsearch leverages primary terms and sequence numbers to identify which operations have already been performed and which operations are required to bring a shard up to date.

To speed up this recovery process, Elasticsearch maintains global and local checkpoints. The global checkpoint represents the sequence number at which all active shards within a replication group are aligned. It signifies that any operations with a sequence number lower than the global checkpoint have already been executed on all shards within the replication group. Similarly, each replica shard maintains a local checkpoint representing the sequence number up to which it has processed operations.

By utilizing primary terms, sequence numbers, and checkpoints, Elasticsearch can efficiently recover from failures and maintain data consistency across shards within a replication group.

It's worth noting that the primary term and sequence number are available within the response to write requests, as well as when retrieving a document by its ID. These fields provide valuable information about the state of the data.


> These notes provide an introductory explanation of how Elasticsearch writes data, focusing on explaining key concepts in a beginner-friendly manner.

## Understanding Optimistic Concurrency Control in Elasticsearch

Optimistic concurrency control is a technique used to prevent older versions of a document from overwriting more recent versions when write operations arrive out of sequence. In a distributed system like Elasticsearch, where network communication is involved, such scenarios can occur.

There are two approaches to implementing optimistic concurrency control in Elasticsearch: the traditional "_version" field and the newer primary terms and sequence numbers. Let's explore both approaches and their usage.

### Approach 1: Using "_version" Field

When indexing a document, Elasticsearch automatically assigns a version number to it. This version is stored in the "_version" field within the document's metadata. Here's an example:

```json
POST /my_index/_doc/1
{
  "name": "John Doe",
  "age": 30
}
```

The response will include the indexed document along with its "_version" field:

```json
{
  "_index": "my_index",
  "_type": "_doc",
  "_id": "1",
  "_version": 1,
  "result": "created",
  "_shards": {
    "total": 2,
    "successful": 1,
    "failed": 0
  }
}
```

To update the document, we include the "_version" field as a query parameter in the update request:

```json
POST /my_index/_update/1?version=1
{
  "doc": {
    "age": 31
  }
}
```

If the supplied version matches the current version stored in the index, the update is successful. Otherwise, Elasticsearch returns an error indicating a version conflict.

### Approach 2: Using Primary Terms and Sequence Numbers

Primary terms and sequence numbers provide a more robust approach to optimistic concurrency control. The primary term represents the number of times the primary shard has changed, while the sequence number represents the order of operations within the primary shard.

When retrieving a document, the response includes the current primary term and sequence number:

```json
GET /my_index/_doc/1
```

The response will contain the document along with the "_primary_term" and "_seq_no" fields:

```json
{
  "_index": "my_index",
  "_type": "_doc",
  "_id": "1",
  "_primary_term": 2,
  "_seq_no": 4,
  "_source": {
    "name": "John Doe",
    "age": 31
  }
}
```

To update the document, we use the "if_seq_no" and "if_primary_term" parameters in the update request:

```json
POST /my_index/_update/1
{
  "doc": {
    "age": 32
  },
  "if_seq_no": 4,
  "if_primary_term": 2
}
```

Elasticsearch verifies that the supplied primary term and sequence number match the current values in the index before allowing the update. If a mismatch occurs, indicating that the document has been modified, the update operation fails with a version conflict error.

### Conclusion

Optimistic concurrency control in Elasticsearch provides mechanisms to prevent data inconsistency when concurrent write operations occur. The "_version" field and primary terms with sequence numbers offer different approaches to achieving this. It's important to choose the appropriate method based on your use case and take into account the benefits and limitations of each approach.

> These notes provide an introductory explanation of optimistic concurrency control in Elasticsearch, emphasizing key concepts and including example code to demonstrate the implementation using both the traditional "_version" field and primary terms with sequence numbers.

## Updating Multiple Documents in Elasticsearch

In Elasticsearch, you can update multiple documents in a single query using the Update By Query API. This functionality is similar to the UPDATE query with a WHERE clause in relational databases. Let's explore how to achieve this.

### Step 1: Constructing the Update By Query Request

To update multiple documents, you need to use the Update By Query API. Start by specifying the HTTP verb and request path.

```json
POST /my_index/_update_by_query
```

In the request body, provide a script for updating the documents. This is done in the same way as updating a single document with a script.

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

### Step 2: Applying a Constraint with a Search Query

To specify which documents should be updated, include a search query in the request. For simplicity, we will use a "match_all" query that matches all documents.

```json
{
  "query": {
    "match_all": {}
  }
}
```

### Step 3: Running the Update By Query

Now that we have defined the update script and query, we can execute the update operation. The response will indicate the number of documents that were updated.

```json
{
  "updated": 2,
  "batches": 1,
  "total": 2,
  "failed": 0,
  "retries": {
    "search": 0,
    "bulk": 0
  },
  "version_conflicts": 0,
  "failures": []
}
```

### Internal Workflow of Update By Query

Internally, the Update By Query API works as follows:

1. A snapshot of the index is created to ensure updates are performed on the current state of the index.
2. A search query is sent to each shard of the index to find the matching documents.
3. The documents are updated in bulk requests sent sequentially to each shard.
4. The query is processed in batches, utilizing the Scroll API to handle large result sets.
5. Elasticsearch automatically retries failed operations up to ten times.
6. If a version conflict occurs during an update, the entire query is aborted.
7. The number of version conflicts is reported in the response.

### Handling Version Conflicts

By default, if a version conflict occurs, the update query is aborted. However, you can specify the "conflicts" parameter with a value of "proceed" to count the version conflicts without aborting the query.

```json
{
  "conflicts": "proceed"
}
```

### Conclusion

Updating multiple documents in Elasticsearch is possible using the Update By Query API. You can provide a script to modify the documents and apply a search query to constrain the update operation. Understanding the internal workflow and handling version conflicts are essential for utilizing this feature effectively.

> These notes provide an explanation of how to update multiple documents in Elasticsearch using the Update By Query API. The step-by-step guide includes example code and details the internal workflow of the update process. It also covers handling version conflicts and provides a conclusion summarizing the key points.

## Deleting Documents with a Condition in Elasticsearch

In Elasticsearch, you can delete documents based on a condition using the Delete By Query API. This allows you to remove multiple documents that match a specific search query. Let's walk through the process.

### Step 1: Constructing the Delete By Query Request

To delete documents, you need to use the Delete By Query API. Start by specifying the HTTP verb and request path.

```json
POST /my_index/_delete_by_query
```

In this example, we will use the "match_all" query to delete all documents within the "products" index. You can replace this query with any other search query as needed.

```json
{
  "query": {
    "match_all": {}
  }
}
```

### Step 2: Running the Delete By Query

Once you have constructed the request, execute the delete operation. The response will indicate the number of documents that were deleted.

```json
{
  "deleted": 2,
  "batches": 1,
  "total": 2,
  "failed": 0,
  "retries": {
    "search": 0,
    "bulk": 0
  },
  "version_conflicts": 0,
  "failures": []
}
```

### Internal Workflow of Delete By Query

The Delete By Query API works similarly to the Update By Query API. Here's an overview of its internal workflow:

1. The API takes a snapshot of the index to ensure deletions are based on the current state.
2. A search query is sent to each shard of the index to find the matching documents.
3. The documents are deleted in bulk requests sent sequentially to each shard.
4. The query is processed in batches using the Scroll API to handle large result sets.
5. Elasticsearch automatically retries failed operations up to ten times.
6. If a version conflict occurs during a delete operation, the entire query is aborted.
7. The number of version conflicts is reported in the response.

### Handling Version Conflicts

By default, if a version conflict occurs, the delete query is aborted. However, you can specify the "conflicts" parameter with a value of "proceed" to ignore version conflicts and continue the deletion process.

```json
{
  "conflicts": "proceed"
}
```

### Conclusion

Deleting documents based on a condition in Elasticsearch is possible using the Delete By Query API. By providing a search query, you can remove multiple documents that match the specified criteria. Understanding the internal workflow and handling version conflicts are crucial for effectively utilizing this feature.

> These notes explain how to delete documents based on a condition in Elasticsearch using the Delete By Query API. The step-by-step guide includes example code and covers the internal workflow of the delete operation. It also discusses handling version conflicts and provides a conclusion summarizing the key points.


## Bulk Operations with the Elasticsearch Bulk API

In Elasticsearch, you can perform bulk operations to index, update, or delete multiple documents at once using the Bulk API. This allows you to efficiently process large volumes of data. Let's explore the Bulk API and its usage.

### Step 1: Constructing the Bulk Request

To perform bulk operations, you need to use the Bulk API. The API accepts a series of actions, each represented by a line in the request body, separated by newline characters (\n or \r\n). The format follows the NDJSON specification.

Start by specifying the HTTP verb and endpoint for the bulk request.

```json
POST /_bulk
```

Each action in the bulk request should be a JSON object containing an action type and associated metadata. The action types include "index," "create," "update," and "delete." Let's begin with the "index" action.

```json
{ "index" : { "_index" : "products", "_id" : "200" } }
{ "field1" : "value1", "field2" : "value2", "field3" : "value3" }
```

In this example, we index a new document with an ID of 200 into the "products" index. The document fields and values are specified in the subsequent JSON object.

### Step 2: Executing the Bulk Request

Once you have constructed the bulk request, execute it. The response will provide detailed information about each action in the "items" key.

```json
{
  "items": [
    { "index": { "_index": "products", "_id": "200", "_version": 1, "result": "created", "status": 201 } },
    ...
  ]
}
```

### Updating and Deleting Documents

You can include multiple actions in the same bulk request. Let's demonstrate updating and deleting documents within a new bulk request.

```json
{ "update" : { "_index" : "products", "_id" : "201" } }
{ "doc" : { "field1" : "updated_value" } }
{ "delete" : { "_index" : "products", "_id" : "200" } }
```

In this example, we update the document with an ID of 201 by specifying the "update" action and the updated fields. Then, we delete the document with an ID of 200 using the "delete" action.

### Additional Considerations

There are a few important points to keep in mind when working with the Bulk API:

1. Set the "Content-Type" header to "application/x-ndjson" to indicate the NDJSON format.
2. Ensure each line in the request body ends with a newline character, including the last line.
3. Errors in individual actions do not affect the other actions in the bulk request.
4. Check the response for detailed information about each action in the "items" key.
5. Bulk operations are more efficient than individual requests, reducing network round trips.
6. You can use routing and optimistic concurrency control by including "if_seq_no" and "if_primary_term" parameters.

### Conclusion

The Bulk API in Elasticsearch allows you to perform efficient bulk operations for indexing, updating, and deleting multiple documents. By structuring the request using NDJSON format and including multiple actions in a single request, you can process large volumes of data effectively.

> These notes explain how to perform bulk operations in Elasticsearch using the Bulk API. The step-by-step guide covers constructing the bulk request, executing it, and handling various actions like indexing, updating, and deleting documents. It also highlights additional considerations and the benefits of using the Bulk API for efficient data processing.


## Importing Test Data using the Bulk API and cURL

In this lecture, we will use the Bulk API along with the cURL command-line tool to import test data into Elasticsearch. This method is suitable for scenarios where you want to perform bulk operations from the command line. Let's go through the process step by step.

### Prerequisites

Ensure that you have cURL installed on your system. Most macOS and Linux distributions already have it preinstalled. If it's not available, you can download it from the official cURL website. Additionally, make sure you have the test data file ready for importing.

### Step 1: Prepare the Test Data File

The test data file should be in NDJSON format, with each line representing a separate action. In this case, we will be using 1000 "index" actions with sequential IDs. Ensure that the file ends with a newline character, which can be achieved by adding an empty line at the end.

### Step 2: Construct the cURL Command

Open a terminal window and navigate to the directory where the test data file is located. Use the `cd` command to change directories. Then, construct the cURL command to send the HTTP request to the Bulk API.

```shell
curl --cacert /Users/adithyanarayanan/Documents/Personal/Internships/Tagit/Elastic\ search/elasticsearch-8.8.2/config/certs/http_ca.crt -u "elastic:IIyVB8_NP=*SxF*fzc7=" -H "Content-Type: application/x-ndjson" -XPOST https://localhost:9200/products/_bulk --data-binary "@products-bulk.json"  
```

In this example, we specify the `-H` option to set the "Content-Type" header as NDJSON. The `-X` option specifies the HTTP verb as "POST." Replace the URL with the appropriate Elasticsearch endpoint for your environment. The `--data-binary` option specifies the test data file name (e.g., "testdata.ndjson").

### Step 3: Execute the cURL Command

Run the cURL command to send the bulk request to Elasticsearch. After a short moment, you will receive a response from the Elasticsearch cluster, indicating the result of the bulk operation.

### Result Analysis

Inspect the response to ensure that the bulk operation was successful. The response will be in the same format as discussed in the previous lecture.

### Verification

To verify the imported data, you can run a search query against the index. The number of documents returned should be 1000, confirming the successful import.

### Conclusion

Using the Bulk API along with the cURL command-line tool, you can easily import large amounts of data into Elasticsearch. By following the steps outlined in this lecture, you can perform bulk operations efficiently from the command line and start working with your test data.

> These notes explain how to import test data into Elasticsearch using the Bulk API and cURL. The step-by-step guide covers preparing the test data file, constructing the cURL command, executing it, and verifying the imported data.


## Introduction to Analysis in Elasticsearch

In this lecture, we will explore the concept of analysis in Elasticsearch, which is specifically applicable to text values. Analysis is the process of transforming text values before storing them in a way that is efficient for searching. Let's dive into the details.

### Text Analysis and the "_source" Field

When indexing a text value, Elasticsearch applies an analysis process to prepare the value for searching. The original text values are stored in the "_source" field of the document, but internally Elasticsearch uses processed values to determine document matches.

### Anatomy of an Analyzer

An analyzer in Elasticsearch consists of three components: character filters, a tokenizer, and token filters. These components work together to transform and tokenize text values.

#### Character Filters

Character filters receive the original text and can modify it by adding, removing, or changing characters. They are applied in the order specified within the analyzer. An example of a character filter is "html_strip," which removes HTML elements and converts HTML entities.

#### Tokenizer

A tokenizer is responsible for tokenizing the text by splitting it into tokens. Tokens are created by removing characters such as punctuation and whitespace. The tokenizer also records the character offsets for each token in the original text.

#### Token Filters

Token filters receive the tokens produced by the tokenizer and can add, remove, or modify them. Like character filters, token filters are applied in the order specified within the analyzer. A common example is the "lowercase" filter, which converts tokens to lowercase.

### Default Behavior: The "standard" Analyzer

By default, Elasticsearch uses the "standard" analyzer for all "text" fields unless configured otherwise. The "standard" analyzer consists of no character filters, the Unicode Segmentation tokenizer, and the "lowercase" token filter. The Unicode Segmentation tokenizer splits text into tokens based on whitespace and hyphens, while the "lowercase" filter converts tokens to lowercase.

### Custom Analyzers

Elasticsearch provides built-in character filters, tokenizers, and token filters that can be combined to create custom analyzers. However, in this lecture, we will focus on the default "standard" analyzer and its behavior.

### Summary

In this lecture, we learned about analysis in Elasticsearch, which is the process of transforming text values before indexing. We explored the components of an analyzer, including character filters, tokenizers, and token filters. The default "standard" analyzer was discussed, which is used for "text" fields unless specified otherwise.

> These notes provide an introduction to text analysis in Elasticsearch. They cover the components of an analyzer, the default behavior of the "standard" analyzer, and the concept of custom analyzers.