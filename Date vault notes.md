# date pipeling

data pipeline is a broad umbrella and ETL is one part of it.

- under a data pipeline, we could have both batch and stream data, whereas under an ETL, you can only have one of these things.
- lambda architecture - batch + stream both in it.
-

what is a data warehouse:

- central repository where all of the data from the different sources resides.
- history is also maintained in the data warehouse.
- business can derive value from that data.

**third normal form(3NF) - also called entity relationship approach:**

- very common modelling technique when it comes to operational system.
- fast writes.
- highly normalized. multiple joins, data to lower grains possible.
- so that business processes can run fast.

**dimensional modelling:**

- use case are users who want to understand business in more detail.
- optimized for reads.
-

**data vault:**

- aims to solve the rigidity that is introduced by only adhering to dimensional modelling or 3nf
- it has three main concepts:
    - hub (business keys)
        - business key that a business can relate and identify with and which is unique for a specific business entity
    - satellite (business contexts of hubs)
        - all other attributes of a business entity, apart from the hub are identified as its satellites.
    - link (relationships between business keys)
        - different hubs of business entities are linked by links, which are unique for each hub pair/relationship.
- there are no deletions in a data vault, only inserts
- data vault architecture is scalable, consistent
