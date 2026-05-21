### 1. Reconnaissance and enumeration - Discover what the application exposes
### 2. Insecure Direct Object Reference (IDOR) - Access data belonging to other users
### 3. Weak password reset - Take over an account through a flawed reset mechanism
### 4. Admin panel access - Escalate from a regular user to an administrator
### 5. Remote code execution - Leverage admin functionality to execute commands on the server

# Reconnaissance and Enumeration
1) Enumeration: nmap -sV -sC -p- 10.67.155.72

  22: SSH
  80: web application running on Apache
  3306: MySQL
  8080: Apache default page
  -> means that the application likely constructs SQL queries, and any input handling weakenesses could lead to SQL-related issues.

2) To check the HTPP response headers: curl -I http://10.67.155.72
  Apache/2.4.58 (Ubuntu)
  PHPSESSID -> this cookie confirms that PHP session management is in use. 

-->> now, Technology Stack: Apache + PHP+MySQL - a classic LAMP Configuration

* LAMP Stack:
  Linux(Operating System)
  Apache(HTTP Webserver)
  MySQL(Database)
  PHP/Pearl/Python(Programming Language)
  -> secure, mature protocol. open source, non-proprietary. flexibility to select the right components for specific projects or business requirements.
  -> Others:WAMP(Microsoft Windows), MAMP(Mac OPS), WIMP(Windows, Internet Information Services webserver from Microsoft)

3) To discover what directories and files exist beyond what the navigtation bar shows: gobuster dir -u http://10.67.155.72 -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -x php -x php

  - /admin - An admin panel exists, but it redirects to the login page. We will need credentials to access it.
  - /api - An API endpoint is present. APIs often expose data in ways the frontend does not.
  - /reset.php - A password reset page. Reset mechanisms are frequently implemented insecurely.
  - /uploads - An uploads directory. If we can upload files, this could be a path to code execution.
  - /profile.php and /dashboard.php - These require authentication, so we need to be logged in to access them.

4) Investigate the api endpoint from gobuster: curl http://10.67.155.72/api/
  {"endpoints":["\/api\/user","\/api\/jobs","\/api\/applications"]}
  -> Already Information Disclosure Issue in a production application



# IDOR
  what we know:  <ins>an authenticated session & the application's structure </ins>

  It uses a predictable identifier to reference objects.

  http://10.67.155.72/profile.php?id=6


# Weak Password Reset






















