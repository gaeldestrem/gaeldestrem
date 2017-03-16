---
title: Elasticsearch 5 - New features 
date: "2016-11-03"
layout: post
path: "/elasticsearch-5"
category: "elasticsearch"
description: "Say heya to the new Elastic Stack (ELK). I'm going to focus on Elasticsearch 5 new features and changes as it the product from the stack I use the most"
---

Say hello to the new Elastic Stack (ELK). I'm going to focus on the new Elasticsearch 5 features and changes as it is the product from the stack I use the most.

<img src="https://i.giphy.com/11sBLVxNs7v6WA.gif" width="500" height="500" />


## New features
### Lucene 6.2

Elasticsearch 5.0.0 will use Lucene 6.2, a major version upgrade of Lucene.

This means big performance improvements!

###  Faster indexing (x2 from Elasticsearch 2)

In version 5.0, Elasticsearch gives shards that have heavy indexing a larger portion of the indexing buffer in the JVM heap.


### New script language : Painless
Elasticsearch 5.0 includes a new scripting language designed to be fast and secure called "Painless".

```
int total = 0;
for (int i = 0; i < doc['things'].length; ++i) {
  total += doc['things'][i];
}
return total;
```

### Pipeline / Ingest node
To pre-process documents before indexing, you define a pipeline that specifies a series of processors. Each processor transforms the document in some way. For example, you may have a pipeline that consists of one processor that removes a field from the document followed by another processor that renames a field. 

Here's an example of a simple pipeline that dynamically adds a field to every indexed document.

```
PUT _ingest/pipeline/my-pipeline-id
{
  "my-pipeline-id" : {
    "description" : "describe pipeline",
    "processors" : [
      {
        "set" : {
          "field" : "foo",
          "value" : "bar"
        }
      }
    ]
  }
}
```

### Index Shrinking
The shrink index API allows you to shrink an existing index into a new index with fewer primary shards.

```
POST my_source_index/_shrink/my_target_index
{
  "settings": {
    "index.number_of_replicas": 1,
    "index.number_of_shards": 1, 
    "index.codec": "best_compression" 
  },
  "aliases": {
    "my_search_indices": {}
  }
}

```
### Rollover index
The rollover index API rolls an alias over to a new index when the existing index is considered to be too large or too old.

```
PUT /logs-000001 
{
  "aliases": {
    "logs_write": {}
  }
}

# Add > 1000 documents to logs-000001

POST /logs_write/_rollover 
{
  "conditions": {
    "max_age":   "7d",
    "max_docs":  1000
  }
}

# Response
{
  "acknowledged": true,
  "shards_acknowledged": true,
  "old_index": "logs-000001",
  "new_index": "logs-000002",
  "rolled_over": true, 
  "dry_run": false, 
  "conditions": { 
    "[max_age: 7d]": false,
    "[max_docs: 1000]": true
  }
}
```

### Re-index from remote
The most basic form of _reindex just copies documents from one index to another. This will copy documents from the twitter index into the new_twitter index

```
POST _reindex
{
  "source": {
    "index": "twitter"
  },
  "dest": {
    "index": "new_twitter"
  }
}
```

Reindex does not attempt to set up the destination index. It does not copy the settings of the source index. You should set up the destination index prior to running a _reindex action, including setting up mappings, shard counts, replicas, etc.


### A new completion suggester

The completion suggester has gained a lot of new features!

- Near-real time
- Deleted document filtering (previously it included deleted documents)
- Multiple context support for filtering
- Regular expression and typo tolerance via regex and fuzzy 
- Context boosting at query time 
- Can now return the entire document in additional phase (payload unneeded)


## Query changes 
- New search_after query for pagination

## Mapping changes
Use either `text` or `keyword` instead of "string" for string fields in mappings
- text means the field is used for full-text search
- keyword means the field will be not analyzed and can be used in aggs or exact matches. 
