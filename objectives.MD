# Installation and Configuration
 * [Deploy and start an Elasticsearch cluster that satisfies a given set of requirements](https://www.elastic.co/guide/en/elasticsearch/reference/current/setup.html)
 * [Configure the nodes of a cluster to satisfy a given set of requirements](https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-node.html)
 * [Secure an Elasticsearch cluster using X-Pack Security](https://www.elastic.co/guide/en/elastic-stack-overview/current/xpack-security.html) +[here](https://www.elastic.co/guide/en/elasticsearch/reference/current/configuring-security.html)
   * select trial license
   * set `xpack.security.enabled: true` in `elasticsearch.yml`
   * [Configure TLS](https://www.elastic.co/guide/en/elastic-stack-overview/current/ssl-tls.html)
   * start ES `./bin/elasticsearch`
   * define passwords `./bin/elasticsearch-setup-passwords interactive`
   * configure Kibana `elasticsearch.username: "kibana"` + `elasticsearch.password: "your_password"`
   * start Kibana `./bin/kibana`
   * [create user](https://www.elastic.co/guide/en/elasticsearch/reference/current/security-api-users.html)
   * [create/assign roles](https://www.elastic.co/guide/en/elasticsearch/reference/current/security-api-roles.html)
 * [Define role-based access control using X-Pack Security](https://www.elastic.co/guide/en/elastic-stack-overview/current/authorization.html#roles) (+[here](https://www.elastic.co/guide/en/elastic-stack-overview/current/mapping-roles.html))

# Indexing Data
 * [Define an index that satisfies a given set of requirements](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-create-index.html)
 * Perform [index](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-index_.html), [create](), [read](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-get.html), [update](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-update.html), and [delete](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-delete.html) operations on the documents of an index
 * [Define and use index aliases](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-aliases.html)
 * [Define and use an index template for a given pattern that satisfies a given set of requirements](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-templates.html)
 * [Define and use a dynamic template that satisfies a given set of requirements](https://www.elastic.co/guide/en/elasticsearch/reference/current/dynamic-templates.html)
 * Use the [Reindex API](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-reindex.html) and [Update By Query API](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-update-by-query.html) to reindex and/or update documents
 * [Define and use an ingest pipeline that satisfies a given set of requirements, including the use of Painless to modify documents](https://www.elastic.co/guide/en/elasticsearch/reference/current/ingest.html)

# Queries
 * Write and execute a search query for [terms](https://www.elastic.co/guide/en/elasticsearch/reference/current/term-level-queries.html) and/or [phrases](https://www.elastic.co/guide/en/elasticsearch/reference/current/full-text-queries.html) in one or more fields of an index
 * [Write and execute a search query that is a Boolean combination of multiple queries and filters](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-bool-query.html)
 * [Highlight the search terms in the response of a query](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-request-highlighting.html)
 * [Sort the results of a query by a given set of requirements](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-request-sort.html)
 * [Implement pagination of the results of a search query](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-request-from-size.html)
 * [Use the scroll API to retrieve large numbers of results](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-request-scroll.html)
 * [Apply fuzzy matching to a query](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-match-query.html#query-dsl-match-query-fuzziness)
 * [Define and use a search template](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-template.html)
 * [Write and execute a query that searches across multiple clusters](https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-cross-cluster-search.html#_using_cross_cluster_search)

# Aggregations
 * Write and execute [metric](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-aggregations-metrics.html) and [bucket](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-aggregations-bucket.html) aggregations
 * [Write and execute aggregations that contain sub-aggregations](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-aggregations.html#_structuring_aggregations)
 * [Write and execute pipeline aggregations](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-aggregations-pipeline.html)

# Mappings and Text Analysis
 * [Define a mapping](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-put-mapping.html) that satisfies a [given set of requirements](https://www.elastic.co/guide/en/elasticsearch/reference/current/mapping.html)
 * [Define and use a custom analyzer that satisfies a given set of requirements](https://www.elastic.co/guide/en/elasticsearch/reference/current/analysis-custom-analyzer.html)
 * [Define and use multi-fields with different data types and/or analyzers](https://www.elastic.co/guide/en/elasticsearch/reference/current/multi-fields.html)
 * [Configure an index so that it properly maintains the relationships of nested arrays of objects](https://www.elastic.co/guide/en/elasticsearch/reference/current/nested.html)
 * [Configure an index that implements a parent/child relationship](https://www.elastic.co/guide/en/elasticsearch/reference/current/parent-join.html)

# Cluster Administration
 * [Allocate the shards of an index to specific nodes based on a given set of requirements](https://www.elastic.co/guide/en/elasticsearch/reference/current/index-modules-allocation.html)
 * Configure [shard allocation awareness](https://www.elastic.co/guide/en/elasticsearch/reference/current/allocation-awareness.html) and [forced awareness](https://www.elastic.co/guide/en/elasticsearch/reference/current/allocation-awareness.html#forced-awareness) for an index
 * Diagnose shard issues and repair a cluster’s health
 * [Backup and restore a cluster and/or specific indices](https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-snapshots.html)
 * [Configure a cluster for use with a hot/warm architecture](https://www.elastic.co/blog/hot-warm-architecture) + [here](https://www.elastic.co/guide/en/elasticsearch/reference/current/shard-allocation-filtering.html)
 * [Configure a cluster for cross cluster search](https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-cross-cluster-search.html#_configuring_cross_cluster_search)
