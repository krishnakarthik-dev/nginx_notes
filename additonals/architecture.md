## **NGINX Architecture**<br>

NGINX is an open source reverse proxy and web server designed for scale. It exploded in popularity as the first line of defense to backend infrastructures. Whether as a caching layer, load balancer, an API gateway or Web server, NGINX does it all.


    * NGINX worker processes
    * Connection Management
    * Request Processing

* **Worker Processes**<br>
    The major part of NGINX architecture is the master process. When you spin up NGINX, it starts a process that manages the rest of processes in NGINX.

    The master process creates two processes for cache management. One for reading the cache from disk and another for refreshing the caches. What interests the most are the worker processes. These are the power horses that do most of the work in NGINX.

    When you set NGINX to auto mode (the default), the application spins up a number of worker processes based on how many CPU cores you have. This changes based on whether you have Hyper-Threading enabled or not.

    Hyper-Threading technology allows a single physical core to appear as two logical cores to the operating system. This can boost performance because the operating system can efficiently schedule processes on multiple hardware CPU threads.

    If you have two-core CPU and hyper-threading is enabled, the OS will see four logical cores or hardware threads. This is a choice you make based on performance.

    Having a one-to-one cardinality between worker process and CPU is a backend choice. This assumes the worker process and requests are CPU-bound which are not necessarily the case. If requests are I/O bound e.g. reading from another backend or database the process spends most of its time doing I/O and not using the CPU. This of course also depends on the protocol used in communication.

* **Connection Management**<br>
    The worker processes listen on their configured port, say it’s 80 for HTTP. The act of listening creates a socket and two queues. One is SYN queue and the other is the ACCEPT queue. Both queues are managed by the kernel.

    If a client connects to port 80, it attempts to establish a TCP connection with the NGINX server. The client sends the SYN beginging the TCP handshake, the kernel receives the SYN and matches it to NGINX listening socket and puts it on the SYN queue. The kernel then replies back with SYN-ACK to complete the TCP handshake. The client finally responds with the ACK to complete the three-way handshake. We no have a full connection.

    Once the connection is complete, the kernel moves the connection to the ACCEPT queue where one of the worker processes picks it up. The worker processes compete for connections on the ACCEPT queue. Was a worker process accepts a connection, a file descriptor is created and now the worker process is responsible for reading data from the connection.

    The worker process can pick up the connection in different ways. Sometimes all the worker processes listen on the same port, and the kernel distributes connections between them. Other times the worker processes have the master worker process accept the connection and it can send the request directly to the worker proces. I discuss this more on here.

    Once worker processes pick up connections they can start reading data. Next is request processing. of course one worker process can accept and handle many connections simultaneously.


* **Request Processing**<br>
    Let’s say two clients are connected to an NGINX load balancer. One client is connected to Worker 3 and the other to Worker 4.

    Client connections live in NGINX workers
    The client on worker 3 sends an HTTP request to fetch an HTML page This is what happens:

        * The request is transmitted as a stream of bytes on the TCP connection
        * The bytes stream arrives at the kernel’s buffer for connection
        * Worker3 calls read on the connection
        * The data is copied to Worker 3’s memory.
        * Worker 3 parsers the data and understands its an HTTP request
        * Worker 3 processes the request and reads from disk to fetch HTML
        * Worker 3 writes back a HTTP response to the connection
        * The response byte stream goes to the send buffer
        * Kernel sends the data to the client

    Note that the kernel never pushes data to the worker processes. Instead, the kernel keeps the data in the receive buffer and tell the worker processes that it has data for it to read.

    Depending on the HTTP version and whether TLS is enabled or not, more work is done by the Worker process to decrypt the data and then parses the protocol. HTTP/2 and 3 are more expensive to parse than HTTP/1.1. This is where pinning a process to a CPU really matters. Having too many processes causes context switches (processes swapped in and out of the CPU) and may slow down performance.

    We can follow the same steps for client connected to Worker 4. The only difference is Worker 4 will establish a new connection to the configured backend to forward the request to. Backend connection pooling is critical to get right here. In fact this is one reason why Cloudflare moved away from NGINX, the backend connection pool could not be easily shared between multiple worker processes.

* NGINX is a powerful web server, load balancer and caching layer.
* The multiple worker architecture allows NGINX to distribute connections and requests across multiple CPUs for more efficient use of resources.
