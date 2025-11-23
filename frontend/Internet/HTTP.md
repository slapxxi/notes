HTTP is a TCP/IP based application layer communication protocol which stands for hypertext transfer protocol.

HTTP is request/response protocol in which you send requests and receive responses.

- SYN - Client picks up a random number, let’s say x, and sends it to the server.
- SYN ACK - Server acknowledges the request by sending an ACK packet back to the client which is made up of a random number, let’s say y picked up by server and the number x+1 where x is the number that was sent by the client
- ACK - Client increments the number y received from the server and sends an ACK packet back with the number y+1

Persistent connections and pipe-lining were added in HTTP 1.1

Chunked Transfers In case of dynamic content, when the server cannot really find out the Content-Length when the transmission starts, it may start sending the content in pieces (chunk by chunk) and add the Content-Length for each chunk when it is sent. And when all of the chunks are sent i.e. whole transmission has completed, it sends an empty chunk i.e. the one with Content-Length set to zero in order to identify the client that transmission has completed. In order to notify the client about the chunked transfer, server includes the header Transfer-Encoding: chunked

Slow responses in HTTP 1.1 can block other resources from loading.

### HTTP 2.0

- Binary instead of Textual
- Multiplexing - Multiple asynchronous HTTP requests over a single connection
- Header compression using HPACK
- Server Push - Multiple responses for single request
- Request Prioritization
- Security
### Headers

### Methods

- get
- post
- head
- put
- delete
- patch
- options