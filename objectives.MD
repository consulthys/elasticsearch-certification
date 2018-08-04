# Disclaimer
This document is not meant as a comprehensive resource for passing the Elastic Certification. Its main goal is to provide a quick cheat sheet of important settings per objective with links and pointers to the Elastic Engineer 1/2 course modules. In order to use this cheat sheet efficiently, one must already have a very good hands-on experience with Elasticsearch.

# Installation and Configuration
 * [Deploy and start an Elasticsearch cluster that satisfies a given set of requirements](https://www.elastic.co/guide/en/elasticsearch/reference/current/setup.html)
   * `cluster.name`
   * `node.name`, `node.attr.xyz`
   * `path.data`, `path.logs`, `path.repo`
   * `network.host`
   * `discovery.zen.ping.unicast.hosts`, `discovery.zen.minimum_master_nodes`
   * `bootstrap.memory_lock`
   * `jvm.options`: heap size (`-Xmx -Xms`), heap dump path (`-XX:HeapDumpPath`), GC logging, fatal error logging (`-XX:ErrorFile`) 
   * File handles in `/etc/security/limits.conf` (`elasticsearch  -  nofile  65536`)
   * Disable swap files in `/etc/fstab` (comment `swap`) / `vm.swappiness=1` / in `/etc/security/limits.conf` (`memlock=unlimited`)
   * Disable swapping in `/etc/security/limits.conf`
   * Increase available threads in `/etc/security/limits.conf` (`nproc=4096`)
   * Increase max file size in `/etc/security/limits.conf` (`fsize=unlimited`)
   * Boost virtual memory in `/etc/sysctl.conf` (`vm.max_map_count=262144`)
 * [Configure the nodes of a cluster to satisfy a given set of requirements](https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-node.html)
   * `node.master`, `node.data`, `node.ingest`, `node.ml`
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
   * `index.number_of_shards`, `index.number_of_replicas`, `index.refresh_interval`
   * `index.max_result_window`, `index.max_inner_result_window`
   * `index.max_script_fields`, `index.max_terms_count`
   * `index.max_ngram_diff`, `index.max_shingle_diff`
   * `index.default_pipeline`
   * `index.blocks.read_only`, `index.blocks.read_only_allow_delete`
   * `cluster.blocks.read_only`, `cluster.blocks.read_only_allow_delete`
   * [more settings...](https://github.com/elastic/elasticsearch/blob/master/server/src/main/java/org/elasticsearch/index/IndexSettings.java)
 * Perform [index](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-index_.html), [create](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-index_.html#operation-type), [read](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-get.html), [update](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-update.html), and [delete](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-delete.html) operations on the documents of an index
   * index: `PUT index/_doc/id`, `POST index/_doc`,
   * create: `PUT index/_doc/id?op_type=create`, `PUT index/_doc/id/_create`
   * read: `GET/HEAD index/_doc/id`, `GET/HEAD index/_doc/id/_source`
   * update: `POST index/_doc/id/_update` with `doc`, `doc_as_upsert`, `script`, `detect_noop`, `upsert`, `scripted_upsert`, `doc_as_upsert`, `POST index/_update_by_query`
   * delete: `DELETE index/_doc/id`, `POST index/_delete_by_query`
 * [Define and use index aliases](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-aliases.html)
   * `POST _aliases`, `PUT/DELETE/GET/HEAD index_name/_alias/alias_name`, `GET/HEAD _alias`
   * actions: `add`, `remove`, `remove_index`
   * properties: `index`, `indices`, `alias`, `filter`, `routing`, `index_routing`, `search_routing`
 * [Define and use an index template for a given pattern that satisfies a given set of requirements](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-templates.html)
   * `PUT/GET/DELETE/HEAD _template/name`
   * `index_patterns`, `aliases`, `settings`, `mappings`, `order`, `version`
 * [Define and use a dynamic template that satisfies a given set of requirements](https://www.elastic.co/guide/en/elasticsearch/reference/current/dynamic-templates.html)
 * Use the [Reindex API](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-reindex.html) and [Update By Query API](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-update-by-query.html) to reindex and/or update documents
   * update by query: `POST index/_update_by_query` with `query`, `script`, `conflicts`, `routing`, `scroll_size`, `pipeline`
   * reindex: `POST _reindex` with `size`, `source{index,type,query,sort,size,remote}`, `dest{index,op_type,version_type,routing,pipeline}`, `conflicts`, `script`, `reindex.remote.whitelist`
 * [Define and use an ingest pipeline that satisfies a given set of requirements, including the use of Painless to modify documents](https://www.elastic.co/guide/en/elasticsearch/reference/current/ingest.html)
   * `PUT/GET/DELETE _ingest/pipeline/id`
   * `POST _ingest/pipeline/_simulate` with `pipeline` and `docs` / `POST _ingest/pipeline/id/_simulate` with `docs`
   * `description`, `version`, `processors`
   * variables: `_source`, `_index`, `_type`, `_id`, `_routing`, `_ingest.timestamp`
   * errors: `on_failure` per processor or global, `_ingest.on_failure_message`, `_ingest.on_failure_processor_type`, and `_ingest.on_failure_processor_tag`
   * [processors](https://www.elastic.co/guide/en/elasticsearch/reference/current/ingest-processors.html): `append`, `convert`, `date`, ...
# Queries
 * Write and execute a search query for [terms](https://www.elastic.co/guide/en/elasticsearch/reference/current/term-level-queries.html) and/or [phrases](https://www.elastic.co/guide/en/elasticsearch/reference/current/full-text-queries.html) in one or more fields of an index
 * [Write and execute a search query that is a Boolean combination of multiple queries and filters](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-bool-query.html)
   * `bool` + `must/must_not/filter/should` with `minimum_should_match` 
 * [Highlight the search terms in the response of a query](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-request-highlighting.html)
   * `highlight`
 * [Sort the results of a query by a given set of requirements](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-request-sort.html)
   * `sort` with `order`, `mode`, `missing`, `unmapped_type`, `_script`, `_geo_distance{order,unit,mode,distance_type}`, `nested{path,filter}`
 * [Implement pagination of the results of a search query](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-request-from-size.html)
   * `from` + `size`
 * [Use the scroll API to retrieve large numbers of results](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-request-scroll.html)
   * `POST index/_search?scroll=1m` with `query`, `slice`
   * `POST _search/scroll` with `scroll` and `scroll_id`
   * `DELETE _search/scroll/scroll_id`, `DELETE _search/scroll/_all`
 * [Apply fuzzy matching to a query](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-match-query.html#query-dsl-match-query-fuzziness)
 * [Define and use a search template](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-template.html)
 * [Write and execute a query that searches across multiple clusters](https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-cross-cluster-search.html#_using_cross_cluster_search)
   * `GET/POST remote:index,index/_search`

# Aggregations
 * Write and execute [metric](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-aggregations-metrics.html) and [bucket](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-aggregations-bucket.html) aggregations
 * [Write and execute aggregations that contain sub-aggregations](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-aggregations.html#_structuring_aggregations)
 * [Write and execute pipeline aggregations](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-aggregations-pipeline.html)

# Mappings and Text Analysis
 * [Define a mapping](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-put-mapping.html) that satisfies a [given set of requirements](https://www.elastic.co/guide/en/elasticsearch/reference/current/mapping.html)
   * `PUT/GET index/_mapping/_doc`, `GET index/_mapping/_doc/field/name`
   * only possible updates:
     * add multi-fields (=> needs reindex)
     * add new properties to `object` type
     * add `ignore_above`
     * set `fielddata: true` (=> no reindex)
 * [Define and use a custom analyzer that satisfies a given set of requirements](https://www.elastic.co/guide/en/elasticsearch/reference/current/analysis-custom-analyzer.html)
   * `type: custom`, 0+ `char_filter`, 1 `tokenizer`, 0+ `filter`, `position_increment_gap` (in case of arrays)
 * [Define and use multi-fields with different data types and/or analyzers](https://www.elastic.co/guide/en/elasticsearch/reference/current/multi-fields.html)
 * [Configure an index so that it properly maintains the relationships of nested arrays of objects](https://www.elastic.co/guide/en/elasticsearch/reference/current/nested.html)
   * `nested` data type (instead of `object`)
   * queries: `nested{path,query}` + `inner_hits` + `nested{path,filter}` sort
   * aggs: `nested{path}`, `reverse_nested{path}`
   * max nested fields per index = 50
 * [Configure an index that implements a parent/child relationship](https://www.elastic.co/guide/en/elasticsearch/reference/current/parent-join.html)
   * `join` data type, `relations` defines the relationships
   * max one `join` field per index
   * parent and child docs must be in same shard (use `routing=parent-id` on GET/DELETE/UPDATE)
   * when indexing parent, only parent relationship is needed
   * when indexing child, child relationship + parent id  + routing id are needed
   * a child can only have one parent
   * queries: `has_child{type,query}`, `has_parent{parent_type,query}`, `parent_id{type,id}`
   * aggs: `children{type}`
# Cluster Administration
 * [Allocate the shards of an index to specific nodes based on a given set of requirements](https://www.elastic.co/guide/en/elasticsearch/reference/current/index-modules-allocation.html)
   * `index.routing.allocation.include.xyz`, `index.routing.allocation.exclude.xyz`, `index.routing.allocation.require.xyz`
   * `cluster.routing.allocation.include.xyz`, `cluster.routing.allocation.exclude.xyz`, `cluster.routing.allocation.require.xyz`
     * `_ip`, `_name`, `_host`, `_host_ip`, `_publish_ip`
   * `index.unassigned.node_left.delayed_timeout`
   * `index.priority`
   * `index.routing.allocation.total_shards_per_node` (index), `cluster.routing.allocation.total_shards_per_node` (global)
 * Configure [shard allocation awareness](https://www.elastic.co/guide/en/elasticsearch/reference/current/allocation-awareness.html) and [forced awareness](https://www.elastic.co/guide/en/elasticsearch/reference/current/allocation-awareness.html#forced-awareness) for an index
   * `cluster.routing.allocation.awareness.attributes`, `cluster.routing.allocation.awareness.force.xyz.values`
 * Diagnose shard issues and repair a cluster’s health
 * [Backup and restore a cluster and/or specific indices](https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-snapshots.html)
   * repo: `PUT/GET/DELETE _snapshot/reponame`, `GET _snapshot/_all`, `POST _snapshot/reponame/_verify`
   * snapshot: `PUT/GET/DELETE _snapshot/reponame/snapshot_name` with `wait_for_completion`, `POST _snapshot/reponame/snapshot_name/_restore`, `GET _snapshot/_status`
   * repo types: 
     * `fs{location,compress,chunk_size,readonly,max_restore_bytes_per_sec,max_snapshot_bytes_per_sec}` + set `path.repo`
     * `url`
     * `s3`, `hdfs`, `azure`, `gcs`
 * [Configure a cluster for use with a hot/warm architecture](https://www.elastic.co/blog/hot-warm-architecture) + [here](https://www.elastic.co/guide/en/elasticsearch/reference/current/shard-allocation-filtering.html)
   * `node.attr.box_type` + `index.routing.allocation.require.box_type`
 * [Configure a cluster for cross cluster search](https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-cross-cluster-search.html#_configuring_cross_cluster_search)
   * `search.remote.xyz.seeds`
   * `search.remote.connections_per_cluster`
   * `search.remote.node.attr`
   * `search.remote.connect`
   * `search.remote.xyz.skip_unavailable`
