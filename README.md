# FOSS Name

## FOSS Project Description and Statistics

## Security Needs

The following outlines basic security needs for three generic Kafka users: Producers, Consumers, and Brokers.

Producers - Clients that publishes data to a specific topic on the server (Kafka cluster) via a broker. This data is stored for a set retention period.

Security Needs of a Producer:

* Encryption of confidential data streamed to a broker.
* Authentication a broker to which data is streamed.
* Confirmation that data was successfully delivered to the broker. 
	
Consumers - Clients that subscribes to various topics within a kafka cluster. The data for a topic is retrieved via a broker and streamed to the consumer.

Security Needs of a Consumer:

* Encryption of confidential data retrieved from a broker.
* Authentication a broker from which data is retrieved.

Brokers - A group of server nodes responsible for read/write operations on specific topic partitions. A broker can be either a leader (which controls read/write operations for a partition) or a replica (which copies partition data for fault-tolerance).

Security Needs of a Broker:

* Encryption of confidential data received, delivered and stored by the broker.
* Authentication of the server on which the broker instance exists.
* Authentication and permission checking of producers trying to write to a broker's assigned topic partitions. 
* Authentication and permission checking of consumers trying to read from a broker's assigned topic partitions.
* Maintaining the integrity of stored data in the case of system failure.



## Security Features 

## Motivation

## License Summary and Contributor Agreement

## Security History

## Links
* [Project Repository](https://github.com/isxbot/software-assurance)
* [Project Kanban](https://github.com/isxbot/software-assurance/projects/1)
