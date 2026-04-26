the architecture : Data Source $\rightarrow$ SQL Transformation $\rightarrow$ Clustering $\rightarrow$ Visualization Output.

we are profiling Network Source IPs to identify different types of devices or behaviors on network.

1. The Database Layer (SQLite)
I used SQLite to handle the data. It is a "SQL-native" database that allows us to run complex queries without a heavy server. This represents the PostgreSQL or BigQuery stage of a modern data pipeline.

SQL Logic: I aggregated over 144,000 rows of traffic by grouping by the Source IP.

Feature Engineering: I calculated total_bytes, packet_count, avg_packet_len, and unique_destinations.

2. The AI & ML Layer (K-Means Clustering)
Using the Scikit-Learn pipeline (the modern industry alternative to Spark MLlib for medium-sized data), I grouped the IPs into 4 behavioral profiles:

Cluster 0 (Background Users): Low volume, consistent communication.

Cluster 1 (The Streamers): Extremely high data volume sent to a single destination.

Cluster 3 (The Hubs): High activity across many different destinations and protocols.

3. Professional Visualization (Seaborn)
For the visualization, I used a Log-Scaled Scatter Plot. Network data often has extreme outliers (one IP sending millions of bytes while others send only 100),
so the log scale ensures we can see every group clearly.

