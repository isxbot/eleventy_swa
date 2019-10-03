## Backstory
Kafka is a distributed streaming platform used to route and process queues of record streams in a fault tolerant manner. It is used for managing data pipelines between systems and applications, as well serving as a platform for building real-time streaming applications.
Kafka is used as a message broker in a wide range of usage environments. Examples include:

*	Implementation on social media platforms to provide on-the-fly ad usage and spend data, using its Streams API.
*	Logging domain level events and site metrics (including user website tracking) via its Consumer API.
*	Connecting database servers to analytics servers via a real-time pipeline, using its Connector API. 

One of the richest environments to implement Kafka’s streaming capabilities is as a middleware application on a social media platform. In such an environment, server integrity, user credentials and site usage metrics, and third-party ad clicks are all examples of attack surfaces for malicious agents or unfortunate happenstances (e.g., equipment failure due to inclement weather).
The stakeholders are the social media users and the site and server administrators, who maintain the hardware, ensure user privacy, and site data availability. Server administrators must correctly configure Kafka servers to treat records appropriately with respect to retention time and topic spooling, among other configurable parameters. Data availability is closely tied into such parameters, and Kafka clusters must be tuned to guarantee topic data is current and pipelined on-demand. The use and misuse cases below illustrate these essential requirements.

## Use Case - Store User Data

The admin in charge of the social media platform’s servers wants to store published user data. This requires that they create a topic on a broker instance to which data (related to that topic) can be published and saved for a set retention period. They want to ensure that the integrity of the data is maintained and neither lost nor corrupted, so that consumers subscribed to the topic can retrieve it. 

#### Misuse Case - Hardware Failure

Hardware issues can cause a server to fail. If that happens, any data stored on that server could be lost.

#### Prevention/Security Requirement

The admin can set up a multi-broker cluster (across multiple machines) so that data can be replicated. This way, if one (or more) machines fails, that data can still be recovered from the machines that still work and are part of the cluster.

#### Misuse Case Evolved

Even if none of the machines fail, if the multi-broker cluster is misconfigured by an mistrained/careless employee, then data published to the topics stored on these brokers might still be lost.

#### Prevention/Security Requirement Evolved

Add some sort of cluster validation test to ensure that a cluster of brokers is correctly configured.

##### Diagram

![Hardware Failure Use Case Diagram](/images/UseCaseDiagram_HardwareFailure.png)
  
#### Advertised Security Features of Kafka

Kafka allows for creating multiple broker instances on a single topic. For a given partition within that topic, one of the brokers is selected as the leader and is responsible for read/write operations. The other brokers are selected as replicas that copy the leader’s data log. If the leader fails, then one of the replicas becomes the new leader. In this way, fault tolerance is improved and data integrity can be preserved in the case of system failures.

#### Configuration Issue

Each broker is configured in a .properties file where the broker id, listening port, and log filename can be set. If two brokers exist on the same machine (for the same topic) and are misconfigured to have the same name for their log file, then they will overwrite each other’s data. This will decrease fault tolerance of stored data by reducing the intended replication. To prevent this, perhaps some sort of check could be added to ensure no brokers for the same topic on the same machine have the same log filename.

## Use Case - Log Aggregation

Sarah, the system administrator at Fakebook needs to aggregate all of the logs from the various subsystems into a single stream to enable lower-latency processing and easier support for multiple data sources, as well as distributed data consumption. Sarah needs the log data to be highly available, so that various systems can perform processes like scanning and sending to long term storage. Additionally, because log accuracy is so important, Sarah needs the aggregated logs to maintain quality (i.e., maintain complete logs with no lapses in log records).

First, Sarah needs to setup a Kafka topic where the subsystems will publish their logs. Then, each subsystem needs to be registered as a producer to allow each system to publish log data to their relevant topic. Sarah also needs to enable authentication on the brokers and producers, as well as create an Access Control List the actions that certain users make on the brokers. Additionally, Sarah will set up replicas to ensure that logs will be available in the event that a broker fails.


#### Misuse Case - Misconfigure Broker Retention Time

Greg is a an employee at Fakebook who recently separated from his girlfriend, who has blocked him on Fakebook. Greg wants to access her personal data, but wants to ensure that he doesn't get caught in the process, as he is not authorized to access user data, configurations, or logs. To avoid detection, Greg will attempt to remove a portion of the aggregated logs via manual deletion and reconfiguration of the Kafka broker.

To do this, Greg needs to reconfigure the Kafka broker hosting the aggregated logs to have a retention time of one millisecond, which will drop the log data from the topic after that time. Additionally, Greg can set the size of records to be kept to 1 byte. Finally, Greg will attempt to manually delete the logs from the broker. These actions will allow Greg to act within the system without the risk of being exposed by the system logs.

#### Diagram
![Use Case/Abuse Case Diagram](/images/UseCaseDiagram_LogAggregation.png)

#### Advertised Security Features of Kafka
Apacha Kafka ships with multiple security features that mitigate or prevent the abuse case from being carried out successfully. Per the documentation:
>Kafka ships with a pluggable Authorizer and an out-of-box authorizer implementation that uses ZooKeeper to store all the ACLs. It is important to set ACLs because otherwise access to resources is limited to super users when an authorizer is configured. The default behavior is such that if a resource has no associated ACLs, then no one is allowed to access the resource, except super users. It is possible to change this behavior, as we discuss below.

Additionally, Kafka includes multiple authentication implementations:
* Encryption and Authorization using SSL
* Authenticatin using SASL
  *  SASL/Kerberos
  * SASL/PLAIN
