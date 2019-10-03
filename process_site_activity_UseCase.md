## Use Case

The system administrator Todd needs to be able to process user site activity in stream format to enable parallel processing which will allow relevant ads to be delivered. 

## Misuse Case

Hacker wants to be able to access user site activity to target a user for exploiting a weak encryption algorithm.

## Prevention/Security Requirement

To prevent this misuse case, encryption should be present in Kafka. A strong encryption algorithm such as TLS 1.2 for encryption in transit would prevent the stream from being accessed to steal the site activity.

## Diagram

![Use Case Diagram](/SiteActivity.jpeg)

## Relevant Advertised Security Features of Kafka

Kafka allows for SSL/TLS to be used for encrytpion in transit between producers/Kafka/and consumers
