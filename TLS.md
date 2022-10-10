# Transport Layer Security (TLS)
TLS is a standard for secure client-server communication.

# How it works
1. Client performs a request to the secure server
2. Server sends it's Certificate and a public key
3. Client creates a symmetric key, encrypts it with the server's public key and
   sends it to the server.
4. Server decrypts client's symmetric key
5. Further communication between client and server can now be fully encrypted
   with this symmetric key.
