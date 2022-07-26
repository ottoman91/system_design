# System Design

## Link

[GitHub - donnemartin/system-design-primer: Learn how to design large-scale systems. Prep for the system design interview. Includes Anki flashcards.](https://github.com/donnemartin/system-design-primer#study-guide)

[https://www.youtube.com/watch?v=-W9F__D3oY4](https://www.youtube.com/watch?v=-W9F__D3oY4)

**Vertical Scaling:**

- Most straightforward approach for scaling.
- You increase disk space, RAM etc.
- But vertical scaling has a ceiling, because at some point you will either exhaust your own finances or the state-of-the-art.
- Throwing money and resources

H**orizontal scaling:**

- understanding that there will be a ceiling, so instead of hitting the ceiling, why dont we try to stay below it and scale our resources to perform well?
- having multiple servers
- we need to have a load balancer so that the traffic coming from clients is distributed across all of the servers.the load balancer has a public IP address, and the servers have private addresses that only load balancers have access to.load balancer can use any number of heurestics to allocate requests to different servers
- BIND DNS server - instead of using a dedicated load balancer, the DNS itself acts as a load balancer and routes the ip address of the server that has a copy of the file. . but just by bad luck, one server might get more complicated requests. roundrobin would still send requests to the server which is handling complicated computations.

**caching:**

- file based caching approach - disadvantage is that space is taking with saving the content. theres redundancy in every single page(e.g header in all places). This also limits the ability to change the aesthetics of a page, now its non trivial. this is perhaps why craigslist looks the same.
- mysql query cache. this enables a query cache, if the query is run again and data isnt changed, it runs it correctly.
- memcached - memory cache. piece of software that works on server and saves stuff in RAM. its a key/value storage mechanism. memcache uses FIFO if the user hasnt accessed data again, in order to maintain the size of memcache function.
- archived tables in mysql - e.g. log values. we can use it for data for diagnostic purposes, we sacrifice read time for long term cost for keeping this record.
-

**load balancer:**

- hardware and software load balancers.

**database replication:**

- either of these files can die, but there is always another copy. theory behind RAID.
- they can reduce the chances of data between shared sessions not disappearing. and they can help with uptime and robustness.
- terminology:
    - master database
    - theres a slave database - slave database makes copies of whatever changes are made in master database.
- replicated databases leads to more redundancy in the data.
- for read-heavy websites, this format works well.
- but data replication still has a single point of failure for write.
- another format - master-master.
- you could have replicate load balancers.

**data partitioning:**

high availability - two masters replicate each other.

**sticky session** :

- if you visit a website multiple times, you will end up on the same session
- we can save the id of a server - but not safe. instead, save a random number, and the load balancer can determine which server this random number corresponds to, this can ensure a sticky session.

## **Scalability for Dummies.**

[https://www.lecloud.net/tagged/scalability/chrono](https://www.lecloud.net/tagged/scalability/chrono)

1. **Clones**
- To make a web service massively scalable, you need to replicate the code/application on multiple servers
- All of the servers are behind a load balancer. The load balancer tracks traffic to the different servers, depending on specific server side rules.
- The servers do not store any user specific information, this is to ensure that the sessions are “sticky” for some time.
- The user specific information eg cookies are either stored on an external persistent cache or an external persistent database
1. **Databases**
- Next step is to scale databases, after scaling the servers and the application, because now the database is the bottleneck as the application scales up.
- there are two methods that can be used:
    - do master-slave replication(read from slave, write to master) and do query optimization, or add more RAM to the database
    - denormalize the database right from the beginning and add no more joins to the table. all the joins would need to be done at the application level. do this method instead of the first one.
- this step would ensure that data is stored persistently and there isnt a single point of failure, but it wont fix things like slow retrieval(read) or write operations in the app. that would be fixed by caching
1. **Cache**
- Its a key-value store, that sits as a layer between the application and the database.
- Whenever the application wants to read data, it should first try to read the data from the cache. If the data is not in the cache, then only should it run the query from the database and then store the results in the cache.
- cache is so fast because it stores all data in RAM
- There are two methods of caching:
    1. Cached database queries(not recommended)
        - this is the most commonly used caching pattern
        - whenever a query is made to the database, the hashed version of the query is the key. if the query is run again, the value is returned from the cache
        - however, this caching technique has issues, especially with expiration. When one value of a cell in the table changes, all of the complicated queries cached need to be changed too.
    2. Cached objects***(preferred)***
        - imagine the data as an object, and store the entire instance of that data object.
        - whenever a change is made to the object, discard the cached object and save it again.
        - this allows for asynchronous processing.

- examples of things to cache:
    - user sessions
    - fully rendered blog articles
    - activity streams
1. Asynchronism
    - Can be of two types:
        - pre-render or complete some basic tasks already, e.g basic html pages of a site can be pre rendered. these tasks are pre-rendered via a cron job, and this improves the speed at which tasks are rendered to end users.
        - there is a job queue, and user’s jobs are immediately sent to the queue to be completed. the main server keeps regularly checking when the job is completed, and as soon as its completed, it lets the user know.

## High Level Tradeoffs

### Performance vs Scalability

- A system is scalable if when resources are increased, it leads to a proportional increase in performance
- If you have a performance problem, your system is slow for a single user
- If you have a scalable problem, your system is fast for a single user but performs poorly under heavy load

### Latency vs Throughout

- Latency is the time to perform some action or to produce some result
- Throughput is the number of such actions that can be performed per unit of time
- generally, one should aim for maximum throughput with acceptable latency

### Availability vs Consistency

### CAP Theorem

We can either get two of Consistency, availability or partition tolerance.

***Consistency*** - each read receives the most recent write or an error

***Availability*** - each request receives a response, without a guarantee that the response would be the latest value

***Partition tolerance*** - the system continues to operate despite arbitrary partitioning due to network outages

We need to support partition tolerance because networks are unreliable. We therefore need to choose between CP or AP

**CP - consistency and partition tolerance**

- Responses might return a timeout error. this design choice is used when our business need requires atomic reads and writes

**AP - availability and partition tolerance**

This is a good choice when the system needs to be working despite external errors or when eventual consistency is fine.

## Consistency Patterns

### Weak Consistency

After a write, reads may or may not see it. A best effort approach is taken. This approach is taken in systems such as memecached. It is also used in ViOP, vide chat and realtime multiplayer games.

### Eventual Consistency

After a write, reads will eventually see the write. Data is replicated asynchronously.  [e.g.in](http://e.g.in) DNS, email.

### Strong consistency

After a write, reads will see it. Data is replicated synchronously. E.g. file systems and RDBMSes. it works well in systems that need transactions.

## Availability Patterns

### Fail-over

1. Active-passive
- heartbeats are sent between teh active and passive server on standby.
- if the heartbeat is interrupted, the passive server takes ownership on sending the data
- This is also known as master-slave failover
1. Active-active
- Both servers are managing traffic, spreading the load between them

**Disadvantages of fail-over pattern:**

- adds more hardware and additional complexity
- there is a potential for loss of data if the active system fails before any newly written data can be replicated to the passive

### Replication

Master-slave and master-master replication

## Load Balancers

They distribute incoming client requests to computing resources such as application servers and databases. They are good at :

- preventing requests from going to unhealthy servers
- preventing overloading resources
- helping to eliminate single points of failures
- ssl termination - decrypting incoming requests and encrypting outgoing responses
- session persistence - issue cookies and route a specific client’s requests to same instance

disadvanges:

- can become performance bottlenecks
- add complexity

Different types of load balancers:

1. Layer 4 - they look at the info in the transport layer, e.g. source, destination IP address, ports in header, but not contents of the package
2. Layer 7 - they look at the application layer to understand how to distribute the requests to the computation resources.

layer 4 require less time and computing resources than layer 7 load balancers.

## Reverse Proxy

 a web server that centralizes all responses from the server side before sending them back to the client. it provides a unified interface to clients.

additional benefits of reverse proxy:

- increased security
- increased scalability
- SSL termination - decrypt incoming requests and encrypt outgoing responses so that the servers dontneed to do these computations.
- compression
- caching
- serve static responses

## Databases

relational databases:

### ACID

**atomicitiy** - each transaction is all or nothing

**consistency** - any transaction will bring the database from one valid state to another

**isolation** - executing transactionns concurrently has same effect as if they were done sequentially

**durability** - once a transaction has been committed, it remains so

ways of scaling databases:

1. master- slave replication
- The master serves reads and writes, replicating writes to one or more slaves, which serve only reads. Slaves can also replicate to additional slaves in a tree-like fashion. If the master goes offline, the system can continue to operate in read-only mode until a slave is promoted to a master or a new master is provisioned.
- disadvantages:
    -
    - There is a potential for loss of data if the master fails before any newly written data can be replicated to other nodes.
    - Writes are replayed to the read replicas. If there are a lot of
    writes, the read replicas can get bogged down with replaying writes and
    can't do as many reads.
    - The more read slaves, the more you have to replicate, which leads to greater replication lag.
    - On some systems, writing to the master can spawn multiple threads to write in parallel, whereas read replicas only support writing
    sequentially with a single thread.
    - Replication adds more hardware and additional complexity.
1. master-master replication
- Both masters serve reads and writes and coordinate with each other on writes. If either master goes down, the system can continue to operate with both reads and writes.
- disadvantages:
    -
    - You'll need a load balancer or you'll need to make changes to your application logic to determine where to write.
    - Most master-master systems are either loosely consistent (violating
    ACID) or have increased write latency due to synchronization.
    - Conflict resolution comes more into play as more write nodes are added and as latency increases.
1. sharding - data is distributed across different databases. leads to lesser number of read or write operations, but more complex application logic and complexity added to the system
2. federation - splits database by function. reduces overall read and write but can lead to expensive joins if a lot of joins and access needs to be made across these different tables.
3. denormalization - improves read performances at the expense of write performances. redundant copies of data are written in multiple tables to avoid expensive joins.
4. SQL tuning. use benchmark(simulate high load situations) and profiling(track performance issues) to identify how to improve a database.

e.g. use CHAR instead of varchar, use indexes on columns that are more commonly searched for or aggregated on in tables, use decimal for currency to avoid floating point representation errors.

## Caching

Client caching

CDN Caching

web server caching - with reverse proxies

database caching

application caching
