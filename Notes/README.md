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

