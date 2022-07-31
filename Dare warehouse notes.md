# data warehousing notes

components of a data warehouse:

1. **operational source systems** - this is where most of the transactions of the business are recorded.
2. **data staging area** - this is where Extract, transform and load of data happens. data staging area is off limits to business users and does not provide query services.
- in data staging area, data might be in normalized form, which reduces the number of writes that need to be made, howvere, reads are expensive from normalized data and in the data presentation layer, data should be dimensionally structured from the normalized structure.
1. **data presentation area**
- this area can be considered as a series of integrated data marts. A data mart is a wedge of the overall presentation area pie. a data mart showcases data from a single business process
- data here must be stored, presented and accessed in dimensional schemas.
- data must also be presented in atomic form, and not just in the form of summaries.
- all data marts must be built using common dimensions and facts - adhere to the data warehouse bus architecture
1. **data access tools**

dimensional modelling vocabulary:

**fact table:**

- it is the primary table in a dimensional model.
- a fact is a business measure.
- a row in a fact table corresponds to a business measure
- all measurements in fact table must be of same grain.
- if there isnt a measuremnt on a specific date, we should keep the fact table blank for that specific row.
- fact tables tend to be deep in number of rows but shallow in number of columns
- fact tables express many-to-many relationships between dimension tables.
- fact tables have at least two foreign keys.
- fact tables have a composite key, that is made out of foreign key combinations
- fact table should have numeric measurements. for textual measurements, try to keep them in dimension tables.
- all fact table grains fall into the following categories:
    - transaction
    - periodic snapshot
    - accumulating snapshot


**dimension table:**

- dimension table is the entry point to the fact table.
- dimension table describes all attributes of the business
- these tables are shallow in terms of number of rows but deep in number of columns. usually around 50-100.
-

**steps for creating a new database:**

1. Select the business process to model
2. declare the grain. preferably the dimensional models should be developed for the most atomic information that is available.
3. choose the dimensions. - identify the primary dimension of the facts table, and then add additional dimensions
4. identify the facts to map in the fact table. all facts should be additive. facts such as percentages and ratios are not additive, so instead, add their numerators and denominators to the facts table instead.

notes:

- avoid null keys in the facts tbale
- have a dimensional table for date, dont rely on business owners being able to query date info from the query itself.
- surrogate keys - keys that are programmatically generated and are not linked with a business logic. all joins between facts and dimension tables should be based on surrogate keys.

terms:

- 3NF modelling - normalization technique that aims to remove data redundancies. It reduces the write operations, but makes read operations extremely complicated. normalized databases are important because update or insert transactions only need to touch the database at one specific point.
- data warehouse bus architecture
- star schemas - if the presentation area is based on a relational database
- cubes - if the presentation layer is based on multidimensional data or online analytic processing(OLAP) technology.
- relational database
