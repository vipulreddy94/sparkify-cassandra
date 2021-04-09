# sparkify-cassandra
 NoSQL Cassandra DB to store data from Sparkify music app

1. Download cassandra and set up a 3 node cluster spread across 2 data centers (nodes cas1 and cas2 in DC1 while node cas3 in DC2) 
  - Set memory in Docker Preferences to 5 GB, as each node might take up around 1.5 GB
  - Pull the Cassandra docker image from the docker registry --> docker pull cassandra. 
  - Run the first container (which is the first node cas1). Name of the cluster is MyCluster and GossipingProtocolFileSnitch is used for communication between          nodes. (-p flag is used to expose ports for networking, and -e flag is used for setting environment variables on the container). 

     container 1
     
     ```
     docker run --name cas1 -p 9042:9042 -e CASSANDRA_CLUSTER_NAME=MyCluster -e CASSANDRA_ENDPOINT_SNITCH=GossipingPropertyFileSnitch -e CASSANDRA_DC=datacenter1 -d cassandra
     ```
  - Run the second and third containers cas2 (datacenter1) and cas3 (datacenter2) with the same clustername MyCluster. 
     
     container 2
     
     ```
     docker run --name cas2 -e CASSANDRA_SEEDS="$(docker inspect --format='' cas1)" -e CASSANDRA_CLUSTER_NAME=MyCluster -e CASSANDRA_ENDPOINT_SNITCH=GossipingPropertyFileSnitch -e CASSANDRA_DC=datacenter1 -d cassandra
     ```
     
     container 3
     
     ```
     docker run --name cas3 -e CASSANDRA_SEEDS="$(docker inspect --format='' cas1)" -e CASSANDRA_CLUSTER_NAME=MyCluster -e CASSANDRA_ENDPOINT_SNITCH=GossipingPropertyFileSnitch -e CASSANDRA_DC=datacenter2 -d cassandra
     ```     
  
  - Reference : https://blog.toadworld.com/2018/02/13/build-a-cassandra-cluster-on-docker 
 
