## **Docker networking**
* httpd is the official apache image

## **Useful debugging tools**
* iputils-ping
* iproute2
* curl
* telnet
* dnsutils
* vim

* THe gateway inside the docker container helps us to connect to the outer wold.
* bridge is the default port
* In linux we can acess this 172.17.0.2 ips since docker is native to linux we cannot do that on mac. In mac the container can send the req outside worls but cannot recieve requests.

* spin two containers form the directory without publishing the ports.
* docker inspect bridge will show us all the container connected to the bridge network
* by default docker uses the bridge network


 ## **Create a network with subnet**
 * docker network create back_net --subnet 30.1.0.1/7

 * each container have their own DNS service provider they share information with each other.

 * If we want the docker not to talk to the external world we can use --internal flag