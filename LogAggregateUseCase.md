## Use Case - Log Aggregation

Sarah, the system administrator at Fakebook needs to aggregate all of the logs from the various subsystems into a single stream to enable lower-latency processing and easier support for multiple data sources, as well as distributed data consumption. Sarah needs the log data to be highly available, so that various systems can perform processes like scanning and sending to long term storage. Additionally, because log accuracy is so important, Sarah needs the data to maintain its integrity.

First, Greg needs to setup a Kafka topic where the subsystems will publish their logs. Then, each subsystem needs to be registered as a producer to allow each system to publish log data to their relevant topic. Finally, Greg needs to setup the systems that will be processing log data as consumers of each log topic.

## Misuse Case

Greg is a bad actor who recently separated from his girlfriend, who has blocked him on Fakebook. Greg wants to access her personal data, but wants to ensure that he doesn't get caught in the process. To do this, Greg needs to reconfigure the Kafka topic hosting the aggregated logs to have a retention time of one millisecond, which will drop the log data from the topic after that time. This will allow Greg to access the user information unnoticed during that time.
