---
layout: post
title:  "Caching Strategies"
author: Xingyan Li
categories: Caching
---
## **Introduction**
Caching is one of the most important mechanisms that is commonly used in software development to improve application performance. The key idea is to store the data in a cache so that it can be accessed quickly in the future. For example, a video playlist recommender system can cache the playlist data in its local memory to avoid computing the results for the same request repeatedly.

## **Two popular types of caching**
1. The first one is local caches. Typically, a local cache allows you to store your frequently used data in the memory of the application server. The advantage of having a local cache within your application is that it can provide you with the most performant and reliable way to access your data. However, a local cache has its own drawback. The data that is stored on each application server cannot be shared, and the capacity of a local cache is limited to the amount of memory that can be used on the application server. [Caffeine](https://github.com/ben-manes/caffeine) is a popular Java caching library that is often used to implement local caches.
2. The second one is remote caches. Unlike local caches that sit within the application, a remote cache is a separate server node (or server nodes) dedicated for storing data in memory. The advantage of remote caches is that they can provide application servers with a centralized view of the cached data. Also, remote caches normally are more scalable than local caches. [Redis](https://redis.io/) is a very popular example of remote caches.

## **Two commonly used caching patterns**
1. The first approach is often referred to as cache-aside/lazy-loading. Given that a cache-aside cache is updated only after the data is requested, it contains only data that the application actually requested. The downside of this lazy-loading approach is that every request will suffer some overhead when the data is not in the cache at the beginning.
2. The second approach is called write-through. The cache is updated whenever the data in the database is updated. This active way of updating the cache keeps the cache up-to-date with the database, which makes it more likely for the data to be found in the cache. However, this approach can be more expensive because it may allow data that is never used to be written to the cache.

## **Cache freshness and TTL**
To maintain the freshness and validity of the cached data, a time to live (TTL) can be applied to cache entries. A cache entry expires automatically after the TTL has elapsed. Normally, the more frequently the data can change, the smaller the TTL should be. 

## **Cache eviction policies**
To prevent the cache size from growing endlessly, some eviction policy can be used to decide which cache entry should be evicted when the cache capacity is reached. Two most common eviction policies are least-recently-used (LRU) and least-frequently-used (LFU).

## **Summary**
In summary, caching often plays an indispensable role in improving the performance of an application. It can help reduce the response time and increase the throughput without adding significant load on either the application server or the backend database. It should be considered when your application is read-heavy and the same data is being accessed frequently.