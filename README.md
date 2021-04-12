# sparkify-cassandra
 - NoSQL Cassandra DB to store data from Sparkify music app. 
 - Data Modeling is done, based on the queries which are to be used. 
 - If other queries are needed due to business requirements, new tables should be modelled and created accordingly. 

1. The python notebook, cassandra-python.ipynb is used to traverse through all the event logs in event_data folder, and create a single new csv file consisting of all the data from all the files.
2. Cassandra DB is connected through the cassandra python driver "cassandra". With the help of this driver, we connect to the cassandra DB on python and create keyspace and tables, and perform insertions and selects. 
3. Based on the given queries, 3 different tabels are modeled to satisfy the business requirements. 
 
