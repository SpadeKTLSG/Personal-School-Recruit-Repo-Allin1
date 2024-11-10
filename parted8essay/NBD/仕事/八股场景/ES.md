‍

‍

‍

# 概念

‍

## 零碎

‍

### 除了ES, 还有啥能应付他的场景(倒排+搜索)

[什么是ClickHouse？ | ClickHouse Docs](https://clickhouse.com/docs/zh)

这种列式数据库, 相较于MySQL这样横过来的数据库是列, 需要一两个字段的内容, 直接一下子出去了.

‍

‍

### ES的query和filter有什么区别

在 Elasticsearch (ES) 中，`query`​ 和 `filter`​ 都用于搜索文档，但它们有一些关键的区别：

1. **评分（Scoring）** ：

    * ​`query`​：会计算相关性评分（relevance score），用于全文搜索和排序。适用于需要根据相关性排序的场景。
    * ​`filter`​：不计算相关性评分，只用于过滤文档。适用于精确匹配和不需要评分的场景。
2. **性能**：

    * ​`query`​：由于需要计算评分，性能相对较低。
    * ​`filter`​：性能更高，因为不需要计算评分，并且可以被缓存。
3. **使用场景**：

    * ​`query`​：适用于需要根据相关性排序的全文搜索。
    * ​`filter`​：适用于精确匹配、布尔逻辑操作和不需要评分的场景。

以下是一个示例，展示了如何在 Elasticsearch 中使用 `query`​ 和 `filter`​：

```json
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "title": "Elasticsearch"
          }
        }
      ],
      "filter": [
        {
          "term": {
            "status": "published"
          }
        }
      ]
    }
  }
}
```

在这个示例中：

* ​`match`​ 查询在 `title`​ 字段中搜索包含 "Elasticsearch" 的文档，并计算相关性评分。
* ​`term`​ 过滤器在 `status`​ 字段中精确匹配 "published" 的文档，不计算相关性评分。

‍

‍

‍

### ES如何处理热key

在 Elasticsearch (ES) 中，处理热键（hot key）问题可以通过以下几种方法来缓解：

1. **使用索引分片**：

    * 将索引分成多个分片（shards），使得查询可以分布到多个节点上，从而减少单个节点的压力。
2. **调整缓存设置**：

    * 增加缓存大小，确保热键的数据可以被缓存，从而减少对磁盘的访问。
3. **使用路由（Routing）** ：

    * 自定义路由策略，将特定的文档路由到特定的分片上，避免某些分片过载。
4. **优化查询**：

    * 使用 `filter`​ 而不是 `query`​，因为 `filter`​ 查询不计算相关性评分，性能更高。
    * 使用 `term`​ 查询进行精确匹配，而不是 `match`​ 查询。
5. **增加副本（Replicas）** ：

    * 增加索引的副本数量，使得查询可以分布到更多的节点上，从而减少单个节点的压力。

‍

‍

‍

## 哪些组件，特点，单机qps多少

‍

组件

1. **Cluster**：簇, 由一个或多个节点组成的集合，提供分布式搜索和索引功能。
2. **Node**：节点, 集群中的一个**实例**，存储数据并参与集群的索引和搜索功能。
3. **Index**：索引, 包含一组相关文档的集合，类似于关系数据库中的表。
4. **Document**：文档, 索引中的基本信息单元，类似于关系数据库中的行。
5. **Shard**：分片, 索引的一个分片，允许水平分割和分布式存储。
6. **Replica**：拷贝, 主分片的副本，用于提高容错性和可用性。

‍

特点

* **分布式**：支持分布式存储和搜索，能够处理大规模数据。
* **高可用性**：通过分片和副本机制，提供高可用性和容错性。
* **实时搜索**：支持实时搜索和分析，适用于需要快速响应的应用场景。
* **RESTful API**：提供简单易用的RESTful API，方便与其他系统集成。
* **全文搜索**：强大的全文搜索功能，支持复杂的查询和分析。

‍

单机QPS    k-10k

‍

### 为什么不能在正常的项目中广泛使用做存储

‍

1. **一致性问题**：ElasticSearch 默认是**最终一致性**模型，这意味着在某些情况下，数据可能不会立即一致。这对于需要强一致性的应用程序来说可能是个问题。
2. **事务支持**：ElasticSearch 不支持**多文档事务**，这意味着你不能在多个文档之间进行原子操作。这对于需要复杂事务处理的应用程序来说是个限制。
3. **数据持久性**：虽然 ElasticSearch 提供了数据持久性，但它的设计初衷是为了搜索和分析，而不是作为主要的数据存储。**数据持久性和恢复机制**不如特定的专门的数据库系统那么强大。
4. **查询复杂性**：ElasticSearch 的**查询语言**（DSL）非常强大，但对于某些复杂的查询，可能不如 SQL 那么直观和高效。
5. **资源消耗**：ElasticSearch 的索引和搜索功能非常强大，但也非常**消耗资源**。对于资源有限的环境，可能不是最佳选择。
6. **安全性**：不如专门的数据库系统那么强大

虽然 ElasticSearch 在某些特定场景下非常有用，比如实时搜索和分析，但在需要**强一致性**、**复杂事务处理**和**高安全性**的应用中，传统的关系型数据库或其他 NoSQL 数据库可能是更好的选择。

‍

‍

‍

‍

# 大块

‍

# 高级

‍

‍

## ES - MySQL哪个快到底咋说

[Link](https://www.zhihu.com/question/637732937/answer/3541788566) 讲得不错

InnoDB也提供了 红黑树结构 的 FTS Index Cache（全文检索索引缓存）来提高性能

“ES是通过倒排索引来实现的查询检索，而MySQL是通过B+ Tree来实现的”这句话，就显得不那么准确了。

甚至MySQL如果可以用到覆盖索引，那连回表操作也都省去了，没准还比ES查询效率更高呢。

So，那ES真的比MySQL快吗？如何从底层实现原理的角度去说服面试官呢？

**性能高的最大原因**

场景下，不仅有千万量级的数据记录，多达二十几个的搜索条件，而且这些搜索项和返回的数据结果并不在一个数据表中，需要进行多表关联查询

由于MySQL InnoDB的联合索引，**很大程度上**是要遵循最左前缀原则的,这就意味着在多维复杂查询的某些场景中，你需要通过（a,b,c）,（a,c,b）,（b,a,c）,（b,c,a）,（c,a,b）,（c,b,a）这种排列组合创建联合索引的方式，保证用户的查询操作可以完全命中索引。

那上述业务场景中有20多个查询项的情况下，通过最左前缀原则、排列组合创建联合索引的方式一定是覆盖不全，况且都不在一个数据库表中，这是更加不可控的。

> Btw：之所以在上文中用到了“很大程度上”，是因为MySQL 8引入了Skip Scan Range Access Method，它在一定条件下可以不遵守最左前缀原则，利用了范围扫描来替代了全表扫描的发生。
>
> 其实现原理为：MySQL隐式的构造了前缀查询条件，使一条查询就变成了多次查询，执行计划type = range。适用于最左条件区分度较低的情况，否则生成SQL过多，与全表扫描相比并无优势。

而该场景下，通过**ES是可以轻松解决**的，其实现机制是“结果合并策略”。

在ES中，**支持 SkipList 和 Bitset 两种方式进行数据结果合并**，前者是采用相互跳跃对比并得出合集的方式，后者则通过倒排列表的值计算出各自的Bitset，并进行AND操作合并。

通过该种方式，则可以轻松解决上述20多个查询项、千万量级数据记录的业务场景中，为其创建索引的问题。

我认为，这就是我们常说的ES比MySQL查询性能高的最大原因。

‍

‍

## es深分页怎么处理

在 Elasticsearch 中，深分页（即从大量结果中获取较高偏移量的结果）可能会导致性能问题，因为它需要跳过大量的文档。以下是几种处理深分页的方法：

‍

### 1. 使用 `search_after`​

​`search_after`​ 是一种基于排序值的分页方式，适用于深分页。它避免了深度分页的性能问题。

```java
SearchResponse response = client.prepareSearch("index")
    .setQuery(QueryBuilders.matchAllQuery())
    .addSort("field", SortOrder.ASC)
    .setSize(10)
    .searchAfter(new Object[]{lastSortValue})
    .get();
```

‍

### 2. 使用 `scroll`​ API

​`scroll`​ API 适用于需要处理大量数据的场景。它会保持一个上下文，允许你逐步获取数据。

```java
// 初始化 scroll
SearchResponse response = client.prepareSearch("index")
    .setQuery(QueryBuilders.matchAllQuery())
    .setSize(100)
    .setScroll(TimeValue.timeValueMinutes(1))
    .get();

// 处理 scroll 结果
while (true) {
    for (SearchHit hit : response.getHits().getHits()) {
        // 处理每个文档
    }
    response = client.prepareSearchScroll(response.getScrollId())
        .setScroll(TimeValue.timeValueMinutes(1))
        .get();
    if (response.getHits().getHits().length == 0) {
        break;
    }
}
```

### 3. 使用 `from + size`​ 结合 `terminate_after`​

对于较浅的分页，可以使用 `from`​ 和 `size`​ 参数，但要注意性能问题。可以结合 `terminate_after`​ 参数限制查询的最大文档数。

```java
SearchResponse response = client.prepareSearch("index")
    .setQuery(QueryBuilders.matchAllQuery())
    .setFrom(1000)
    .setSize(10)
    .setTerminateAfter(10000)
    .get();
```

‍

### 4. 使用 `search_after`​ 和 `point in time`​ (PIT)

结合 `search_after`​ 和 `point in time`​ (PIT) 可以在深分页时保持一致性。

```java
// 创建 PIT
CreatePitResponse pitResponse = client.admin().indices().prepareCreatePit("index")
    .setKeepAlive(TimeValue.timeValueMinutes(1))
    .get();

// 使用 PIT 和 search_after
SearchResponse response = client.prepareSearch("index")
    .setQuery(QueryBuilders.matchAllQuery())
    .addSort("field", SortOrder.ASC)
    .setSize(10)
    .setSearchAfter(new Object[]{lastSortValue})
    .setPit(pitResponse.getId())
    .get();
```

这些方法可以帮助你在处理 Elasticsearch 深分页时提高性能和效率。
