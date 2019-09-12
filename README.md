# Apache Kafka

## Description and Statistics

Kafka is a distributed steaming platform that functions as a messaging system, storage system, and as a stream processor. For messaging, Kafka can do both scale processing and multi-subscriber at the same time. For Kafka as a storage system, Kafka stores and replicates all data to disks for redundancy and allows for the users to requests an acknowlegement to ensure the write occured. In regards to Kafka as a stream processor, Kafka can read streams in real-time. Adding all three together you have a piece of software that is able to store and porcess both future messages and historical messages in an efficient manner. Kafka is a tailorable open source software that can be used on many platforms. 

**Activity and Contributors**: 
Kafka has an active community and has 579 contributors as of September of 2019. Shown in the photo below, retrieved from [openhub](https://www.openhub.net/p/apache-kafka) you can see the activity rise.
![Activity](/KafkaActivity.png)

 **Popularity**
Kafka is a popular open source software with more than 13,477 stars on github and 7,000 forks as of September of 2019. Kafka is used by a lot of big companies such as Pinterest, The New York Times, Adidas, Rabobank, Box, Ancestry, Airbnb, Cisco, Netflix, Oracle, Paypal, and many more. You can find the full list [here:](https://kafka.apache.org/powered-by)

**Languages Used**
The majority of the language used with Kafka is Java, however, many other languages are used as well. These langugages consist of Scala, HTML, Python, Shell Script, XML, DOS Batch Script, XSL Transformation, Ruby, and JavaScript. Below is a chart detailing the above. This chart was retrieved from [openhub](https://www.openhub.net/p/apache-kafka)
![Languages](/KafkaLanguages.png)

**Documentation Sources**

Kafka has very extensive documentation, all documentation can be found [here](https://kafka.apache.org/documentation)

## Operational Environment

Kafka is useful for building and handling real-time streaming pipelines constructed between applications and their underlying systems, and for building applications that will appropriately manipulate such data. Kafka achieves these goals through its four core APIs:

**The Producer API:** Allows applications to publish record steams to Kafka topics.

**The Consumer API:** Allows applications to subscribe to topics and process the records stored within them.

**The Streams API:** Allows an application to process streams input from one or more topics, and then create output streams to other topics.

**The Connector API:** Allows construction of producers and consumer applications that link Kafka topics to other applications and systems.

The aforementioned APIs of Kafka have a wide range of use cases that require appropriate security measures.  One example is implementation as a message broker.  Message brokers are middleware program modules that translate messages using the sender's protocol, to the receiver's protocol.  Messages have headers, key byte blocks, and value byte blocks, each of variable length, all of which require an adequate encryption and authentication mechanisms via SSL. SSL requires generation of public-private key pairs associated with a given certificate for each broker in the transaction.  Kerberos is another authentication protocol that provides adequate encryption between broker and producer or consumer.  Without message brokers, many service platforms would become untenably complex for use with messaging via TCP or HTTP.

Social media platforms (SMPs) can make use of the Kafka Streams API to deliver spend data to ad servers.  SMPs suffer from ad overdelivery, which refers to ads that are shown for customers whose budgets have been depleted. Kafka's Streams API mitigates loss-of-revenue from overdelivery, by doing the following:

* Work for different types of ads, such as static ads, and those that integrated event-handlers.
* Handle many thousands of events per-second.
* Rapidly update delivery to thousands of client machines within ten seconds or less.
* Have no downtime.
* Offer a lightweight infrastructure with easy maintenance.

Kafka's millisecond delay guarantee and portable Java architecture is easily disseminated and maintained, and is ideal for constucting a predictive spend pipeline solution, which lessens ad overdelivery.

## Security Needs

The following outlines possible security needs for three generic Kafka users: producers, consumers, and brokers.

Producers - clients that publishes data to a specific topic on the server (Kafka cluster) via a broker. This data is stored for a set retention period.

Security Needs of a Producer:

* Encryption of confidential data streamed to a broker.
* Authentication of brokers to which data is streamed.
* Confirmation that data was successfully delivered to the broker. 
	
Consumers - clients that subscribes to various topics within a kafka cluster. The data for a topic is retrieved via a broker and streamed to the consumer.

Security Needs of a Consumer:

* Encryption of confidential data retrieved from a broker.
* Authentication of brokers from which data is retrieved.

Brokers - a group of server nodes responsible for read/write operations on specific topic partitions. A broker can be either a leader (which controls read/write operations for its partitions) or a replica (which copies partition data for fault-tolerance).

Security Needs of a Broker:

* Encryption of confidential data received, delivered and stored by the broker.
* Authentication of the server on which the broker instance exists.
* Authentication and permission checking of producers trying to write to a broker's assigned topic partitions. 
* Authentication and permission checking of consumers trying to read from a broker's assigned topic partitions.
* Maintaining the integrity of stored data in the case of system failure.

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
There were multiple factors that were evaluated during project selection. 

First, the team wanted an open source project that is relevant in the real world, i.e. something that software engineers and cyber security specialists are likely to encounter in a professional setting. Our goal is to make the exercise of the software assurance process to be as real as possible.

Next, the team evaluated the software as to whether it would be a good candidate for our exercise by looking at technical requirements and features related to security (security features and needs). The team also wanted to ensure that the software was written in a language that all members are familiar with, as well as a language that is supported by tools used to assess software analysis like OpenSCAP and SWAMP.

Apache Kafka is a good fit for both of the teams requirements because it is a software that is being used by small and large organizations in different production environments, and some of the team members have already encountered Kafka in a professional setting. This makes Kafka a good fit as a realistic example of a software assurance case.

Kafka also lends itself to the team's second criteria, as it has multitple security requirements and features in place. The software is used to stream massive amounts of data to multiple clients, and the data is often sensitive in nature, so it is critical that data security and integrity is maintained. This makes for a good exercise in software assurance.

Additionally, Kafka is mostly written in the Java programming language (followed by Kotlin), which all team members are familiar with. Given the popularity of Java and Kotlin, both languages are supported by tools used to analyze code, which will provide the team with necessary tools to complete a thorough software assurance process.

## License Summary and Contributor Agreement
**License**

Kafka uses Apache license 2.0. This allows for commercial use, modification, distribution, patent use, and private use. The limitations on this license prevents against trademark use, liability, and warranty. 

**Procedures for Making Contributions**
Kafka has very detailed contributing instructions that are located [here](https://kafka.apache.org/contributing/html) and [here](https://cwiki.apache.org/confluence/display/KAFKA/Contributing+Code+Changes)

**Contributor Agreements**
The agreement states that when contributing code you are affirming that the contribuiton is yours and that you license the work to the project and have the legal authority to do so.
## Security History

Kafka has had few security fixes implemented for subsequent releases, which are documented in their [security vulnerability](https://kafka.apache.org/cve-list) page. If a possible vulnerability is suspected, it is reported to the [Apache Software Foundation](security@kafka.apache.org), after which a security team works with the reporter to resolve it. Verified vulnerabilities are fixed, followed by a publically announced new release.  

Thus far, only three vulnerabilites have been reported and patched for subsequent releases.  The first was  CVE-2017-12610, which allowed Kafka clients to impersonate another user by using a manufactured protocol message in SASL/PLAIN or SASL/SCRAM authentication, while using the native Kafka PLAIN and SCRAM implementations.  The second was CVE-2018-1288, which let clients perform broker-privileged actions using a fetch request that corrupted data replication, causing data loss.  The most recent was CVE-2018-17196; this vulnerability enabled users to create a "produce" request that compromised the transaction ACL validation mechanism. Summaries for the three vulnerabilites are seen below.

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
