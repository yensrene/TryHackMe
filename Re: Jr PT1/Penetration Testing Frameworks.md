## Table of Contents
- **Open Source Security Testing Methodology Manual**
- **OWASP Web Security Testing Guide**
- **NIST Special Publication 800-115**
- **Penetration Testing Execution Standard**
- **Information Systems Security Assessment Framework**

### Benefits of a structured methodology
- thoroughness: critical areas are not overlooked
- consistency: different testers on the same team produce comparable results
- compliance: aligning the assessment with regulatory requirements
- communication: clients, auditors, and stakeholders can understand and trust a process grounded in a recognized standard.

# OSSTMM
**Open Source Security Testing Methodology Manual** developed by the Institue for Security and Open Methodologies (ISECOM)

- Human Security (HUMSEC): Social engineering and human-factor vulnerabilities
- Physical Security (PHYSSEC): Physical access conrtols, from badge readers to tailgating.
- Wireless Communications (SPECSEC): Wi-Fi, Bluetooth, RFID, and other electromagnetic signals
- Telecommunications (COMSEC): Phone systems, VoIP, fax, and modem infrastructure
- Data Networks (DATASEC): Network services, firewalls, and application-layer protocols


#Recap

### C2 Evasion Technique
- Domain Generation Algorithm: Creates thousands of domains with few registered
- Fast Flux: Rapidly changes IP addresses for one domain
- DNS Tunnelling: Hides data in DNS queries
- HTTPS Encryption: Encypts command and control traffic

### Steps to compromise a web application through vulnearbility chaining
1. Enumerate directories and discover admin panel
2. Exploit IDOR to discover administrator email
3. Reset admin password using exposed token
4. Upload web shell through admin file upload

### Broad coverage helps assess the overall security posture rather than focusing on single attack paths.'

### HTTP Method
- DELETE: DELETE requests remove resources but do not upload files.
- HEAD: HEAD requests retrieve headers only and cannot upload files.
- GET: GET requests retrieve data from servers but cannot upload files.
- OPTIONS: OPTIONS requests query server capabilities but do not upload files.
- POST: POST request are used to submit data including file uploads to web servers.
