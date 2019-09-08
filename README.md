# Apache Kafka

## FOSS Project Description and Statistics

## Security Needs

## Security Features
Because Apache Kafka is used to stream mission-critical data including personally identifiable information, confidential information, and Department of Defense classified Secret and Top Secret information, data integrity and security is essential.

Kafka uses _authentication, authorization, and encryption_ to secure its clusters and data within. Per the [documentation](https://kafka.apache.org/documentation/#security), Kafka includes the following security features:
1. Authentication of connections to brokers from clients (producers and consumers), other brokers and tools, using either SSL or SASL. Kafka supports the following SASL mechanisms:
    * SASL/GSSAPI (Kerberos) - starting at version 0.9.0.0
    * SASL/PLAIN - starting at version 0.10.0.0
    * SASL/SCRAM-SHA-256 and SASL/SCRAM-SHA-512 - starting at version 0.10.2.0
    * SASL/OAUTHBEARER - starting at version 2.0
2. Authentication of connections from brokers to ZooKeeper
3. Encryption of data transferred between brokers and clients, between brokers, or between brokers and tools using SSL (Note that there is a performance degradation when SSL is enabled, the magnitude of which depends on the CPU type and the JVM implementation.)
4. Authorization of read / write operations by clients
5. Authorization is pluggable and integration with external authorization services is supported

These features can be omitted or used in conjunction with each other in whatever way is best suited for the environment; "non-secured clusters are supported, as well as a mix of authenticated, unauthenticated, encrypted and non-encrypted clients."

## Motivation

## License Summary and Contributor Agreement

## Security History

## Links
* [Project Repository](https://github.com/isxbot/software-assurance)
* [Project Kanban](https://github.com/isxbot/software-assurance/projects/1)
