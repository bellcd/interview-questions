# Caching

1. How does caching work on a server layer?
   1. storing some data in memory, RAM, commonly in a key-value store like redis or memcache, so that it's faster to access than having to read that same data from disk through a database
2. What are several caching invalidation strategies?
   1. time based (10s, 60s, 30days, etc..)
   2. least recently used - LRU - (ie, evict the video that was accessed the longest time ago)
   3. least frequently used - LFU - (ie, evict the video that accessed the least)