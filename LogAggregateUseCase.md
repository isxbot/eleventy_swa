## Use Case - Log Aggregation

Sarah, the system administrator at Fakebook needs to aggregate all of the logs from the various subsystems into a single stream to enable lower-latency processing and easier support for multiple data sources, as well as distributed data consumption. Sarah needs the log data to be highly available, so that various systems can perform processes like scanning and sending to long term storage. Additionally, because log accuracy is so important, Sarah needs the data to maintain its integrity.

First, Sarah needs to setup a Kafka topic where the subsystems will publish their logs. Then, each subsystem needs to be registered as a producer to allow each system to publish log data to their relevant topic. Finally, Sarah needs to setup the systems that will be processing log data as consumers of each log topic.

#### Misuse Case - Misconfigure Broker Retention Time

Greg is a bad actor who recently separated from his girlfriend, who has blocked him on Fakebook. Greg wants to access her personal data, but wants to ensure that he doesn't get caught in the process. To do this, Greg needs to reconfigure the Kafka topic hosting the aggregated logs to have a retention time of one millisecond, which will drop the log data from the topic after that time. This will allow Greg to access the user information unnoticed during that time.

#### Diagram
![Use Case/Abuse Case Diagram](/images/UseCaseDiagram_LogAggregation.png)Greg

#### Advertised Security Features of Kafka
Apacha Kafka ships with the security features necessary to avoid this abuse case from being carried out. Per the documentation:
>Kafka ships with a pluggable Authorizer and an out-of-box authorizer implementation that uses ZooKeeper to store all the ACLs. It is important to set ACLs because otherwise access to resources is limited to super users when an authorizer is configured. The default behavior is such that if a resource has no associated ACLs, then no one is allowed to access the resource, except super users. It is possible to change this behavior, as we discuss below.

Additionally, Kafka includes multiple authentication implementations:
* Encryption and Authorization using SSL
* Authenticatin using SASL
  *  SASL/Kerberos
  * SASL/PLAIN
