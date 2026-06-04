# Table of Contents
- HTTP
- FTP
- POP3
- SMTP
- IMAP

## SMTP (Simple Mail Transfer Protocol

Components:
1. MUA: Mail User Agent (ex: Thunderbird, Outlook, webmail interface)
2. MSA: Mail Submission Agent
3. MTA: Mail Transfer Agent
4. MDA: Mail Delivery Agent

Email Protocols:
- **SMTP: Simple Mail Transfer Protocol**
- **POP3: Post Office Protocol version 3**
- **IMAP: Internet MEssage Access Protocol)**

SMTP Ports:

|Number|Encryption|
|-----|----|
|25|optional and negotiated via STARTTLS|
|587|TLS encryption is negotiated via the STARTTLS command|
|465|TLS encryption begins immediately upon connection|

## POP3 (Post Office Protocol 3)
> a protocol used to download email messages from a Mail Delivery Agent(MDA) server. 

|Number|Encryption|
|110|upgrading the connection to TLS using the STLS command|
|995|connection is encrypted from the start|


Common POP3 Commands
|Command|Description|
|-----|------|
|USER username|Identifies the user|
|PASS password|Authenticates with the password|
|STAT|Returns the number of messages and the total size|
|LIST|Lists all messages with their sizes|
|RETR n|Retrieves message number n|
|DELE n|Marks message n for deletion|
|RSET|Resets messages marked for deletion|
|QUIT|Ends the session and deletes marked messages|

Download the message
