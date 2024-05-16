## **TLS (Traansport Layer Security)**
* used for end-to-end-encryption
* Symmetric encryption (client and server has the same key) - fast
* Asymmetric encrytion (diffie heellman) - slow

## **TLS Termination**
* nginx has a tls(https) backend is not  http
    * nginx terminates the TLS and decrypts and send unencrypted message
* nginx is a tls and backend is also a tls. recommented while hosting in cloud.
    * nginx terminates the tls, decryptes, maybe add headders and reencrypt to the backend/ additional laetncy. AES is good. RSA is bad.
* nginx can look at data but it needs to share the backend certificates. some people dosent allow that

## **TLS Passthrough**
* backend is https
* nginx just pipes the packets directly to the https backend. a man in the middle
* no caching
* more secure



