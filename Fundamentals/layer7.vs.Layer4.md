## **Layer 4 vs Layer 7**
* refers to OSI model
* know where the client is going
* Require decryption
* share backend connection
* caching results
* add more headers
* nginx more efficient in layer 7 at the cost of decrytion
* Layer one - radio or light signals
* Layer two - mac address
* Layer three - Ip
* Layer four - TCP Ip
* Layer five - session layer
* Layer six - presentation layer
* Layer seven - application layer

## **Layer 4**
* Source IP, Source Port
* Destination IP, Destination Port
* Simple packet inspection (SYN/TLS hello)

* can operate on Layer 7 (http) and Layer 4 (tcp)
* Layer 4 proxying is useful when the nginx doesn't understand the protocol (database protocol) 
