# FOSS Name

## FOSS Project Description and Statistics

## Operational Environment

Apache Kafka is a distributed streaming platform that offers three main functions that include the capability of publishing and subscribing to a record stream; the corresponding ability to store such streams in a secure manner with appropriate fault-tolerance measures, and the capacity to process live streams.   Therefore, Kafka is useful for building and handling real-time streaming pipelines constructed between applications and their underlying systems, and for building streaming applications that will appropriately manipulate such data. Kafka runs as a cluster on servers and stores data streams as *records*, which are categorized as distinct *topics*. 

The four APIs at the heart of Kafka include the following:

**The Producer API:** Allows applications to publish record steams to Kafka topics.
**The Consumer API:** Allows applications to subscribe to topics and process the records stored within them.
**The Streams API:** Allows an application to process streams input from one or more topics, and then create output streams to other topics.
**The Connector API:** Allows construction of producers and consumer applications that link Kafka topics to other applications and systems.

The aforementioned functions of Kafka have a wide range of use cases that require appropriate security measures.  One example is implementation as a message broker.  Message brokers are middleware program modules that translate messages using the sender's protocol, to the receiver's protocol.  Messages have headers, key byte blocks, and value byte blocks, each of variable length, all of which require an adequate encryption and authentication mechanisms via SSL. SSL (secure sockets layer) is a technology that establishes an encrypted link between two agents. This process involves generation of public-private key pairs for each certificate, for each broker in the transaction.

Without message brokers, many service platforms would become untenably complex for use with messaging via TCP or HTTP.  Stock trading applications rely on message brokers to serve as a hub for opening and securing message channels, through which trade requests travel.  Cloudflare uses Kafka to process and store analytics logs on the order of hundreds of billions of events, per day.  Many other services use Kafka, or similar middleware, and all require secure communication pipelines between brokers and clients.

## Security Needs

## Security Features 

## Motivation

## License Summary and Contributor Agreement

## Security History

Kafka has had few security fixes implemented for subsequent releases, which are documented in their [security vulnerability](https://kafka.apache.org/cve-list) page. If a possible vulnerability is suspected, it is reported to the [Apache Software Foundation](security@kafka.apache.org), after which a security team works with the reporter to resolve it. Verified vulnerabilities are fixed followed by a publically announced new release.  

Thus far, only three vulnerabilites have been reported and patched for subsequent releases.  The first was  CVE-2017-12610, which allowed Kafka clients to impersonate another user by using a manufactured protocol message in SASL/PLAIN ir SASL/SCRAM authentication, while using the native Kafka PLAIN and SCRAM implementations.  The second was CVE-2018-1288, which let clients perform broker-privileged actions using a fetch request that corrupted data replication, causing data loss.  The most recent was CVE-2018-17196; this vulnerability enabled users to create a "produce" request that compromised the transaction ACL validation mechanism. Summaries for the three vulnerabilites are seen below.

| CVE-2017-12610     |                                               |
| ------------------ | --------------------------------------------- |
| Versions affected  | 0.10.0.0 to 0.10.2.1, 0.11.0.0 to 0.11.0.1    |
| Fixed versions     | 0.10.2.2, 0.11.0.2, 1.0.0                     |
| Impact             | Issue could result in privilege escalation.   |
| Issue announced    | 26 July 2018                                  |


| CVE-2018-1288      |                                               |
| ------------------ | --------------------------------------------- |
| Versions affected  | 0.9.0.0 to 0.9.0.1, 0.10.0.0 to 0.10.2.1,     |
|                    | 0.11.0.0 to 0.11.0.2, 1.0.0                   |
| Fixed versions     | 0.10.2.2, 0.11.0.3, 1.0.1, 1.1.0              |
| Impact             | Issue could potentially lead to data loss.    |
| Issue announced    | 26 July 2018                                  |


| CVE-2018-17196     |                                               |
| ------------------ | --------------------------------------------- |
| Versions affected  | 0.11.0.0 to 2.1.0                             |
| Fixed versions     | 2.1.1 and later                               |
| Impact             | Issue could result in privilege escalation.   |
| Issue announced    | 10 July 2019                                  |

## Links
* [Project Repository](https://github.com/isxbot/software-assurance)
* [Project Kanban](https://github.com/isxbot/software-assurance/projects/1)
