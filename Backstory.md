## Backstory
Kafka is a distributed streaming platform used to route and process queues of record streams in a fault tolerant manner. It is used for managing data pipelines between systems and applications, as well serving as a platform for building real-time streaming applications.
Kafka is used as a message broker in a wide range of usage environments. Examples include:

*	Implementation on social media platforms to provide on-the-fly ad usage and spend data, using its Streams API.
*	Logging domain level events and site metrics (including user website tracking) via its Consumer API.
*	Connecting database servers to analytics servers via a real-time pipeline, using its Connector API. 

One of the richest environments to implement Kafka’s streaming capabilities is as a middleware application on a social media platform. In such an environment, server integrity, user credentials and site usage metrics, and third-party ad clicks are all examples of attack surfaces for malicious agents or unfortunate happenstances (e.g., equipment failure due to inclement weather).
The stakeholders are the social media users and the site and server administrators, who maintain the hardware, ensure user privacy, and site data availability. Server administrators must correctly configure Kafka servers to treat records appropriately with respect to retention time and topic spooling, among other configurable parameters. Data availability is closely tied into such parameters, and Kafka clusters must be tuned to guarantee topic data is current and pipelined on-demand. The use and misuse cases below illustrate these essential requirements.