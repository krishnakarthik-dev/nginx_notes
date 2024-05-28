* Client req header is a time out for reading the request client header
* if the client doesnt transmit the entire header with this time the request is terminated and send back with a 408 error.
* Default time out is set to 60 seconds.
* This feature comes in handy to prevent against the slowloris DDoS attact.