# Apache Kafka

## FOSS Project Description and Statistics

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

## Links
* [Project Repository](https://github.com/isxbot/software-assurance)
* [Project Kanban](https://github.com/isxbot/software-assurance/projects/1)
