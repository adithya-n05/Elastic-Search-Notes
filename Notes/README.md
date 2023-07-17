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
```