References : https://leetcode.com/discuss/career/229177/My-System-Design-Template
https://github.com/donnemartin/system-design-primer#how-to-approach-a-system-design-interview-question

1. **Outline use cases, constraints and assumptions**
    - Who would use the system?
    - What are the system inputs and outputs?
    - How many people will use it?
    - Outline use cases that would be covered
    - Outline use cases that won’t be covered.
2. **Estimations**
    - What is the throughput?
    - what latency is expected from the system for read/write transactions?
    - what is the read/write ratio?
    - what is the traffic estimation, for write and read?
    - what are storage estimates?
    - what is memory storage requirements?
        - if we are using cache, what kind of data do we need to cache?
        - how much RAM and how many machines do we need?
        - what amount of data do we need to store in SSD/RAM?
3. **Design goals**
    - latency vs throughput requirements (maximal throughput and minimal latency thats fine)
    - what is the consistency(weak/strong/eventual) and availability(fail over/replicate) design considerations?

4. **high level design**
    - what are the APIs for read/write scenarios for crucial components?
    - what is the database schema?
    - what is the high level design for read/write operations?

1. **deep dive**
    - scaling the algo
    - scaling individual components
    - consistency and availability design decisions
    - think about all of the following components:
        - DNS
        - CDN(push vs pull)
        - load balancers(active-passive, active-active, layer 4, layer 7)
        - reverse proxy(if applcable)
        - DB(RDBMS or NOSQL)
            - RDBMS - sharding, federation, master-slave, master-master, denormalization, sql tuning
        - nosql
            - key-value, document, graph
        - cache(client, CDN, webserver caching, db caching, application caching)
        - asynchronism
            - message queues
2. **justification of key ideas**
