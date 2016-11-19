# Cache

## Problem
- Performance in communication with external services

## Solution


## Application

There are different approaches for caching data:

* Programmatic caching strategy (in-memory hash table)
* Programmatic transparent [Memoization](https://en.wikipedia.org/wiki/Memoization)
* Local cache service
* Distributed Cache server

## Impact


### Available tools
* Microsoft AppFabric
* In-memory databases
* Memcached
* Redis
* Ehcache


### Notes
Microsoft does not promote Fabric anymore

https://docs.microsoft.com/en-us/azure/redis-cache/cache-faq#which-azure-cache-offering-is-right-for-me

## PoC

Ok

| Feature                 | AppFabric   | Ezcache   | Hazelcast      | Redis   |  Memcached  |
| ----------------------- |:-----------:| :-------: | :-------------:| :-----: | :---------: |
| Key/Value store         | yes         |           |                |   yes   |   yes       |
| Complex data types      |             |           |                |   yes   |   no        |
| Platform independent    |             |           |                |   yes   |   yes       |
| Multi-threading         |             |           |                |   no    |   yes       |
| Licence                 | Commercial  |  Both     |                |   OS    |   OS        |


When it comes to boosting application performance through caching, Redis and Memcached are the most established and production-proven candidates. 

### Requirements

* Throughput increases linearly with the increase of number of shards
* Single shard, about 50K RPS
* platform independent (C#, Java, others)
* Available on cloud
* Locally installable (or local emulator) for local testing
* Available in containers
* Security requirements: ask Boris
  * support for SSL
  

### Support
Used by many companies and in countless mission-critical production environments, both Memcached and Redis are supported by client libraries in every conceivable programming language, and it's included in a multitude of packages for developers. In fact, it's a rare Web stack that does not include built-in support for either Memcached or Redis. 

### AppFabric Cache
* Clustering built-in (very simplified management)
* Very easy to setup and configure in Windows machines
* It supports cache expiration (TTL)
* 

### In-memory Databases
* More sofisticated way to retrieve data other that key/value
* 




### Enterprise Ehcache / Software AG
* Part of the Terracotta stack;
* Ehcache is an open source cache for Java. It has been bought by Terracotta Inc. (2009); Terracotta Inc. has been acquired by Software AG in 2011;
* Clustering built-in (very simplified management)
* Pure key/value store: more complex data structure must be serialized;
* No internal scripting language
* No referential integrity
* Support for composite keys
* Embeddable
* Only one replication model: Symmetric Replication


### Memcached
* Developed since 2003, very stable and well supported
* Only support string datatype. For other datatypes, serialization is needed
* Can have fragmentation issue with moderate large amount of data
* Being multithreaded, it scales up pretty well
* Only Data Eviction mechanism based on lazy Last Recently Used (LRU)
* Keys limited to 250 bytes
* Technology stack agnostic: it supports .NET, ASP.NET, Java, Node.js, and Python.

### Redis
* Single threaded: scales ony with clustering without loss of data.  Clustering is an effective scaling solution, but it is comparatively more complex to set up and operate compared to multithreading. 
* Richer data structures
* Smart data eviction algorythms, with fine-grained control
* Keys limited to 512MB
* Data structures are not opaque (i.e., the server can manipulate them)
* Server side scripting (via Lua scripting language)
* Technology stack agnostic: it supports .NET, ASP.NET, Java, Node.js, and Python.
* Not embeddable
* Several Replication models
    Master-Slave Replication
    Asynchronous replication
    Multi-master replication

#### Ops
* Supported on Azure (it's the default cache directly managed by Microsoft)
* Data persistency: designed to bootstrap the cache after a planned shutdown or an unplanned failure. While we tend to regard the data in caches as volatile and transient, persisting data to disk can be quite valuable in caching scenarios. Having the cache's data available for loading immediately after restart allows for much shorter cache warm-up and removes the load involved in repopulating and recalculating cache contents from the primary data store. 
* Data replication for implementing High Available Cache, that can withstand failures and provide uninterrupted service to the application
* Clusters support sharding
* Monitoring: Redis provides a slew of metrics and a wealth of introspective commands with which to monitor and track usage and abnormal behavior. Real-time statistics about every aspect of the database, the display of all commands being executed, the listing and managing of client connections -- Redis has all that and more. 
* Also a good fit for analytics
* When using extremely large operational data sets or analytics workloads, running everything in-memory might not be cost effective. To achieve submillisecond performance at lower cost, Redis Labs created a version of Redis that runs on a combination of RAM and flash, with the option to configure RAM-to-flash ratios.
* Secuity and Network Isolation: 

## References

[Why Redis beats Memcached for caching](http://www.infoworld.com/article/3063161/application-development/why-redis-beats-memcached-for-caching.html)
[Azure Caching Official Documentation](https://docs.microsoft.com/en-us/azure/redis-cache/cache-faq#which-azure-cache-offering-is-right-for-me)
[Picking Your Cache](https://www.brentozar.com/archive/2012/05/picking-your-cache/)
