## Use Case - Store User Data

The admin in charge of the social media platform’s servers wants to store published user data. This requires that they create a topic on a broker instance to which data (related to that topic) can be published and saved for a set retention period. They want to ensure that the integrity of the data is maintained and neither lost nor corrupted, so that consumers subscribed to the topic can retrieve it. 

## Misuse Case - Hardware Failure

Hardware issues can cause a server to fail. If that happens, any data stored on that server could be lost.

## Prevention/Security Requirement

The admin can set up a multi-broker cluster (across multiple machines) so that data can be replicated. This way, if one (or more) machines fails, that data can still be recovered from the machines that still work and are part of the cluster.

## Misuse Case Evolved

Even if none of the machines fail, if the multi-broker cluster is misconfigured by an mistrained/careless employee, then data published to the topics stored on these brokers might still be lost.

## Prevention/Security Requirement Evolved

Add some sort of cluster validation test to ensure that a cluster of brokers is correctly configured.

## Diagram

![Hardware Failure Use Case Diagram](/images/UseCaseDiagram_HardwareFailure.png)
  
## Advertised Security Features of Kafka

Kafka allows for creating multiple broker instances on a single topic. For a given partition within that topic, one of the brokers is selected as the leader and is responsible for read/write operations. The other brokers are selected as replicas that copy the leader’s data log. If the leader fails, then one of the replicas becomes the new leader. In this way, fault tolerance is improved and data integrity can be preserved in the case of system failures.

## Configuration Issue

Each broker is configured in a .properties file where the broker id, listening port, and log filename can be set. If two brokers exist on the same machine (for the same topic) and are misconfigured to have the same name for their log file, then they will overwrite each other’s data. This will decrease fault tolerance of stored data by reducing the intended replication. To prevent this, perhaps some sort of check could be added to ensure no brokers for the same topic on the same machine have the same log filename.
