
## **AWS Redshift Deep Dive**

**LastUpdate:** July 08, 2019

- **AWS Online Tech Talk**:
    - [link](https://www.youtube.com/watch?v=Hur-p3kGDTA)
    - Presenter: **Tony Gibbs**
    - Date: Aug 23, 2018

- **Content**:
    - Started as a fork of PostgreSQL, but was modified to a Columnar store ![](images/columnar_terminology.png) ![](images/columnar_data.png)
    - Massive Parallel Processing **MPP**, scale horizontally up to 2PB of Raw storage
    - Support OnLine Analytical Processing **OLAP** Functions
    - Support the AWS Ecosystem ![](images/redshift.png)
    - Started in Feb 2013, patches usually every 2 weeks (within the 30 mins maintenance window)

- **Terminology and Concepts**:
    - Architecture: ![](images/redshift_arch.png)
    - Compression:
        - Definition: ![](images/compression_terminology.png)
        - Example: ![](images/compression_example.png)
        - Best Practices: [Column Encoding Utility](https://github.com/awslabs/amazon-redshift-utils/tree/master/src/ColumnEncodingUtility)
    - Blocks:
        - Definition: ![](images/blocks_terminology.png)
    - Zone Maps:
        - Definition: ![](images/zone_maps_terminology.png)
    - Data Sorting:
        - Definition: ![](images/data_sorting_definition.png)
        - Example by two sorting columns: ![](images/data_sort_example.png)
        - Example with Zone Maps and Sorting: ![](images/data_sorting_zone_maps_example.png)
        - best practices:
            - [filter](https://github.com/awslabs/amazon-redshift-utils/blob/master/src/AdminScripts/filter_used.sql)
            - [predicate_columns](https://github.com/awslabs/amazon-redshift-utils/blob/master/src/AdminScripts/predicate_columns.sql)
    - Slices:
        - Definition: ![](images/slices_terminology.png)
        - Data Distribution: ![](images/slices_data_distribution.png)
            - Example ALL: ![](images/slice_data_distribution_style_ALL_example.png)
            - Example EVEN: ![](images/slice_data_distribution_style_even_example.png)
            - Example KEY **Wrong**: ![](images/slice_data_distribution_style_key_example_wrong.png)
            - Example KEY **Good**: ![](images/slice_data_distribution_style_key_example_good.png)
            - Best Practices: ![](images/slice_data_distribution_best_practices.png)
        - Summary: ![](images/slice_data_distribution_summary.png)
    - Disks:
        - Definition: ![](images/disks_terminology.png)
    - Redundancy:
        - Definition: ![](images/redundancy_terminology.png)
    - Transactions:
        - Definition: **ACID** (Atomicity, Consistency, Isolation, Durability)![](images/transactions_terminology.png)
        - [commit_statistics](https://github.com/awslabs/amazon-redshift-utils/blob/master/src/AdminScripts/commit_stats.sql)


**Data Ingestion**
- Considerations: ![](images/data_ingestion_considerations.png)
- COPY Statement: 
    - Comparison: ![](images/data_ingestion_COPY_statement.png)
    - Best Practices: ![](images/data_ingestion_COPY_best_practices.png)
- Spectrum: ![](images/data_ingestion_with_spectrum.png)
- Deduplication / UPSERT: ![](images/data_ingestion_deduplication-UPSERT.png)
- Best practices: ![](images/data_sort_best_practices.png)

**ELT: Extract Transform Load**
- Concepts: [ETL/ELT](https://aws.amazon.com/mp/scenarios/bi/etl/) ![](images/etl_vs_elt.png)
- Read the [paper](docs/etl_vs_elt_aws.pdf)
- Best Practices: ![](images/ELT_best_practices.png)

**Vacuum and Analyse**
- Definition: ![](images/vacuum_and_analyze.png)
- [vacuum_utility](https://github.com/awslabs/amazon-redshift-utils/tree/master/src/AnalyzeVacuumUtility)

**Work Load Management (WLM)**
- Definition: ![](images/work_loads_management_wlm.png)
- Concepts: ![](images/wlm_concepts.png)
- Example Configuration: ![](images/wlm_example_conf.png)
- Example: ![](images/wlm_example.png)
- Query Monitoring Rules QMR: ![](images/query_monitoring_rules_qmr.png)
- Best Practices: ![](images/wlm_qmr_best_practices.png)
    - leave about 5% of non assigned memory, so each queue can do first serve
    - [wlm](https://github.com/awslabs/amazon-redshift-utils/blob/master/src/AdminScripts/wlm_apex_hourly.sql)

**Node Types**
- Dense Compute DC2: Solid State disks
- Dense Storage DS2: Magnetic disks
- **Note**: Using S3 as a tier storage coupled with Spectrum is considered like another type of storage
- Cluster Sizing: ![](images/cluster_sizing_best_practice.png)


**Resources:**
- Blogs:
    - [Table Design](https://aws.amazon.com/blogs/big-data/amazon-redshift-engineerings-advanced-table-design-playbook-preamble-prerequisites-and-prioritization/)
    - [Tunning](https://aws.amazon.com/blogs/big-data/top-10-performance-tuning-techniques-for-amazon-redshift/)
    - [Spectrum](https://aws.amazon.com/blogs/big-data/10-best-practices-for-amazon-redshift-spectrum/)
    - [BigData Blog](https://aws.amazon.com/blogs/big-data/)
- Code:
    - [amazon-redshift-utils](https://github.com/awslabs/amazon-redshift-utils)
    - [aws-lambda-redshift-loader](https://github.com/awslabs/aws-lambda-redshift-loader)
    - [amazon-redshift-monitoring](https://github.com/awslabs/amazon-redshift-monitoring)
    - [aws-servicebroker-redshift](https://github.com/awslabs/aws-servicebroker-redshift)