---
layout:     post
title:      2020-08-14-HTTP Essential Training
subtitle:   RESTful Developer Path 02
date:       2020-08-14
author:     BY Elon
header-img: img/post-bg-coffee.jpg
catalog: true
tags:
    - Web Development
    - REST
    - HTTP
---
1. What's protocol?
A protocol in information system means a system of rules that allow communication of information between different entities, like computers.
2. What's hypertext?
Hypertext is somewhat outdated word for text that is displayed on a computer screen that contains hyperlink to other texts. aka, Web Documents.
3. Hypertext transfer protocol
A set of rules that allow web documents to be transferred back and forth in the computer network. HTTP contains below principles:
	- *Plain language and human-readable*: such as http methods (GET, PUT, POST, DELETE, CONNECT, HEAD) which is easy to understand.
	- *Stateless*: each individual http request sent over the protocol is unique and no request is connected to another request. HTTP has no memory for previous requests. This ensures that users don't get trapped in or placed in the middle of sequences of contents, but it also means that you can't walk their way through sequences because the requests are not connected.
	- *Session*: to fix stateless, HTTP allows sessions, storing states shared between the browser and the server. The browser and the server could exchange information about where the visitor is in the sequence by **cookies**. HTTP is stateless, but not sessionless. That passing of cookies allows HTTP to preserve sessions.
	- *HTTP HEADERs*: it can contains,
		* what type of client sent the request
		* server configuration
		* time and date of the response
		* duration of data storage
		* data format
		* cookies used to track sessions
	- HTTP works based on request/response pairs.

4. HTTP, HTTP/2, HTTPS
- HTTP/1.1: 
	- uncompressed headers
	- transfers one file at a time
	- no default encryption
- HTTP/2 is more secure and faster than 1.1 because it uses compression alg to speed up request, allows for multi-plexing, meaningful multiple files are sent over connect at the same time and requires an encrypted connection between the client and the server thru HTTPS.
- HTTPS
5. HTTP Terms
- TCP
short for *Transmission Control Protocol*, one of the main internet protocols used by the Wordl Wide Web, email, FTP, and remote administration.
- IP
short for *Internet Protocol*, IP is used to actually transfer data between computers over a network. Every device connected to the internet has an IP address.
- URL
*Unified Resource Locator*, an address pointing at a resource on the web.
- DNS
*Domain Name Space*, DNS catalogs all domain name URLs and points them to the IP address of servers, physical address 192.144.2.456 etc IPv4, IPv6.
- Proxy
software or hardware service acting as a middle person between clients and servers. Proxy are often used when the IP address of server need to be hidden or when a server or client sits behind some of network barriers like a firewall.
- Header
Request or Response Headers contains metadata about the request or response.
- Cache
Method for storing data on the client or the server to speed up performance.
- Cookie
String of data passed back and forth between clients and servers to create a stateful session.
- Session
clients and servers can share information about states by passing information back and forth, creating a session.

6. HTTP flows
	1. Client/Browser opens a TCP connection to the server to ensure data can be sent back and forth over the network and that the data sent from one end is put together the same way at the other end. If the connection happens over HTTPS, TLS-*[Transport Layer Security](https://en.wikipedia.org/wiki/Transport_Layer_Security#:~:text=Transport%20Layer%20Security%20(TLS)%2C,security%20over%20a%20computer%20network.)* certificates are exchanged to ensure only the computer and the server can encrypt and decrypt the transmitted data.
	2. The browser sends an HTTP message. It always contains an HTTP method, like GET, PUT, DELETE or similar and a URL pointing at the requested resource. It can also contains headers like cookies or authentication data and data.
	3. The server performs the requested actions and sends a response back to the browser. It can contain an HTTP status message, headers and requested data.
	4. Once the HTTP response is received, The TCP connection is closed.

7. Anatomy of a URL
	* Protocol declaration, like http or https
	* Domain - a DNS registered name, usually pointing to a server
	* Port - hidden by default :80 for http, :443 for https
	* Resource path - a ideal path pointing to a resource
	* URL queries - optional, like "?uid=123&udate=20201008" is used to track user id or filter contents or other actions.