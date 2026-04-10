# Protocols and Servers

## Table of Contents

- Telnet(#Telnet)
- Hypertext Transfer Protocol
- File Transfer Protocol
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

### Hypertext Transfer Protocol

It's used to transfer web pages. Not Encrypted.
<img width="1016" height="333" alt="image" src="https://github.com/user-attachments/assets/ca9ab517-8b5f-4281-ba54-f3c21b58c318" />

Using Telnet of Netcat, you can communicate with a web server and act as a "web browser". So you need to input HTTP-related commands instead of the web browser. 

Ex) Using telnet to request a page from a web server.
1. connect to port 80 > telnet MACHINE_IP 80
2. Type > GET /index.html HTTP/1.1 to retrieve the page index.html or GET / HTTP/1.1 to retrieve the default page.
3. Provide some value for the host like > host: telnet and press the Enter key twice.
