## TCP and UDP

### TCP (Transmission Control Protocol)

TCP, or Transmission Control Protocol, is a connection-oriented protocol used for reliable and ordered communication between devices on a network. It provides mechanisms for establishing and maintaining a connection, as well as ensuring that data packets are delivered in the correct order and without errors. TCP is commonly used for applications that require high reliability, such as web browsing, email, file transfer (FTP), and remote login (SSH).

### UDP (User Datagram Protocol)

UDP, or User Datagram Protocol, is a connectionless protocol used for sending datagrams (packets) of data over a network. Unlike TCP, UDP does not establish a connection before sending data and does not guarantee delivery or order of packets. It is often used in applications where speed and efficiency are more important than reliability, such as real-time multimedia streaming, online gaming, and DNS (Domain Name System) lookups.

### Commonly Used Ports on the Web

- **HTTP (Hypertext Transfer Protocol)**:
  - TCP port 80 (HTTP) - Default port for serving web pages over the internet.
- **HTTPS (Hypertext Transfer Protocol Secure)**:
  - TCP port 443 (HTTPS) - Secure version of HTTP, used for encrypted communication over the internet.
- **FTP (File Transfer Protocol)**:
  - TCP port 21 (FTP Control) - Used for control commands in FTP.
  - TCP port 20 (FTP Data) - Used for data transfer in FTP.
- **SSH (Secure Shell)**:
  - TCP port 22 (SSH) - Secure protocol for remote login and command execution.
- **SMTP (Simple Mail Transfer Protocol)**:
  - TCP port 25 (SMTP) - Used for sending email messages between servers.
- **POP3 (Post Office Protocol version 3)**:
  - TCP port 110 (POP3) - Used for retrieving email from a server.
- **IMAP (Internet Message Access Protocol)**:
  - TCP port 143 (IMAP) - Used for retrieving email from a server, with more features than POP3.
- **DNS (Domain Name System)**:
  - UDP/TCP port 53 (DNS) - Used for translating domain names to IP addresses.

These are just a few examples of commonly used ports on the web. There are many other ports used for various applications and services, each serving a specific purpose in the world of networking and internet communication.
