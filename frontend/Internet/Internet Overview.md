![[Pasted image 20250520223931.png]]

- no one specific is in charge
- ARPANET defense department
- nation wide experimental packet network
- fully distributed, no central server/whatever

### Implementation

- bits over the metaphorical wire
- bit rate
- latency
- signal loss
- electricity/radio/light
- light is fast and allows sending multiple bits with different angles, less signal loss as well

### IP & DNS

- IP - internet protocol
- DNS - domain name system

### Packets, Routing, Reliability

- IP packets of information
- routers route traffic i.e. packets over the network
- TCP - transmission control protocol
- TCP reassembles packets in order to reconstruct the information sent
- if packets are missing TCP won't sign making the sender send missing packets again
- the main principles are fault-tolerance and reliability

Three way handshake. TCP connections begin with a three-way handshake in which the client and the server share a series of packets before starting to share the application data.

### HTTP & HTML

- URL - uniform resource locator
- client/server
- HTTP - hypertext transfer protocol
- cookies
- SSL - secure sockets layer
- TLS - transport layer security which is SSL's successor
- active when used with HTTPS
- provides digital certificate which is like an ID card
- certificates are published by digital authorities, trusted entities that verify identities of websites and issue certificates for them
- handshake is used to exchange information to negotiate the encryption algorithm and other parameters for the secure connection

For secure connections established over HTTPS, another "handshake" is required. This handshake, or rather the [TLS](https://developer.mozilla.org/en-US/docs/Glossary/TLS) negotiation, determines which cipher will be used to encrypt the communication, verifies the server, and establishes that a secure connection is in place before beginning the actual transfer of data. This requires five more round trips to the server before the request for content is actually sent.

### Encryption and Public Keys

- encryption/decryption
- key is crucial for encryption algorithms
- today encryption uses 256 bit keys
- symmetric encryption is when receiver and sender use the same key
- asymmetric encryption is when keys are different for encrypting and decrypting
- public and private keys are used
- public key is used to encrypt data and everybody can use it to encrypt data
- the secret can only be decrypted by the computer with the private key

