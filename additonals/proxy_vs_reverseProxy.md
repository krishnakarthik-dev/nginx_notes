## **proxy**
* takes the client to fox example google.com. The server doesnt know where or who the client is
* it helps to prevent from entering certain websites
* we can use it as caching
* use it as the cached content
* Helps in looging all the requests
* where microsrevices are used

## **reverse proxy**
* client doesnt know the final destination
* reverse proxy routes the requests to various backends load balancing.
* Helps in caching
* Ingress give seperates routes to seperate backends which helps in the balancing the loads effeciently we can give high resource consuming api to one server. This comes in application in Kubernetes and Containerisation
* Canaray Deployment Eg: 3 % of the users should go to the newly deployed server

* Both can be used at the same time for that we call a service mesh
* VPN is more secure than a proxy since vpn can only see the domain of the website