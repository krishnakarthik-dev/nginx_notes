## **Workers**
* if you have four cores we can have 8 worker cores
* 4 hardware threads 4 worker processes
* kernel is placed behind the worker processes
* ngnix says to the kernel to redirect the request. if the request comes to a certain port say port 80. so when the request arries it is the kernel who redirect the req to the nginx.
* there are syn que and accept queue when the 3 way handshake is completed the req is then moved to the accept queue
* nginx is responsible to get the connection from the accept queue
* worker consome the connection and decides what to do
* 1 cpu core for one worker
* try to do one to one mapping
* example one worker will communicate with backend while the other servers the web content 
* 1 workers can have many connections