# Protocols and Servers
- If cleartext(or not encrypted), use telnet or netcat. 
## Table of Contents

- [Telnet](#Telnet)
- [Hypertext Transfer Protocol](#HTTP)
- [File Transfer Protocol](#FTP)
- Simple Mail Trnasfer Protocol
- Post Office Protocol 3
- Internet Message Access Protocol

### Telnet

It's used to connect to a virtual terminal of another computer. Not Encrypted.

For the Users:
-> asked for a username and password.
-> listen for incoming connections on port 23. 

It is no longer secure, anyone capturing your network traffic will discover your username and passwords.
Instead SSH is used. 

### HTTP

It's used to transfer web pages. Not Encrypted.
<img width="1016" height="333" alt="image" src="https://github.com/user-attachments/assets/ca9ab517-8b5f-4281-ba54-f3c21b58c318" />

Using Telnet of Netcat, you can communicate with a web server and act as a "web browser". So you need to input HTTP-related commands instead of the web browser. 

Ex) Using telnet to request a page from a web server.
1. connect to port 80 > telnet MACHINE_IP 80
2. Type > GET /index.html HTTP/1.1 to retrieve the page index.html or GET / HTTP/1.1 to retrieve the default page.
3. Provide some value for the host like > host: telnet and press the Enter key twice.

Three popular choices for HTTP servers:
1. Apache
2. Internet Information Services (IIS)
3. nginx

The most popular web browsers:
1. Chomme by Google
2. Edge by Microsoft
3. Firefox by Mozilla
4. Safari by Apple


### FTP

It was developed to transfer files between different computers with different systems efficient. 
Also, it sends and receives data as cleartext. -> FTP server & FPT client

* port 21 is default.
* 
