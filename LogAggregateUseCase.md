## Use Case - Log Aggregation

Sarah, the system administrator at Fakebook needs to aggregate all of the logs from the various subsystems into a single stream to enable lower-latency processing and easier support for multiple data sources, as well as distributed data consumption. Sarah needs the log data to be highly available, so that various systems can perform processes like scanning and sending to long term storage. Additionally, because log accuracy is so important, Sarah needs the aggregated logs to maintain quality (i.e., maintain complete logs with no lapses in log records).

First, Sarah needs to setup a Kafka topic where the subsystems will publish their logs. Then, each subsystem needs to be registered as a producer to allow each system to publish log data to their relevant topic. Sarah also needs to enable authentication on the brokers and producers, as well as create an Access Control List the actions that certain users make on the brokers. Additionally, Sarah will set up replicas to ensure that logs will be available in the event that a broker fails.


#### Misuse Case - Misconfigure Broker Retention Time

Greg is a bad actor who recently separated from his girlfriend, who has blocked him on Fakebook. Greg wants to access her personal data, but wants to ensure that he doesn't get caught in the process, so he wants to remove a portion of the aggregated log records. To do this, Greg needs to reconfigure the Kafka topic hosting the aggregated logs to have a retention time of one millisecond, which will drop the log data from the topic after that time. Additionally, Greg can set the size of records to be kept to 1 byte. Finally, Greg will attempt to manually delete the logs from the broker. These actions will allow Greg to act within the system without the risk of being exposed by the system logs.

#### Diagram
![Use Case/Abuse Case Diagram](/images/UseCaseDiagram_LogAggregation)

#### Advertised Security Features of Kafka
Apacha Kafka ships with multiple security features that mitigate or prevent the abuse case from being carried out successfully. Per the documentation:
>Kafka ships with a pluggable Authorizer and an out-of-box authorizer implementation that uses ZooKeeper to store all the ACLs. It is important to set ACLs because otherwise access to resources is limited to super users when an authorizer is configured. The default behavior is such that if a resource has no associated ACLs, then no one is allowed to access the resource, except super users. It is possible to change this behavior, as we discuss below.

Additionally, Kafka includes multiple authentication implementations:
* Encryption and Authorization using SSL
* Authenticatin using SASL
  *  SASL/Kerberos
  * SASL/PLAIN
