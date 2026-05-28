# Cyber Kill Chain
  It is a cybersecurity framework introduced by Lockheed Martin in 2011.
  1. Reconaissance: gathers information about the target
  2. Weaponisation: make the payload
  3. Delivery: sends the weaponised payload to the target
  4. Exploitation: exploits a vulnearbility in the target's system.
  5. Installation: enables the attacker to install a backdoor or malware to maintain persistence in the target's environment
  6. Command & Conrtol: conrols the compromised system using the backdoor.
  7. Actions on Objectives: carry out further actions such as data exfiltration or other system's exploitation

## 1) Reconnaissance
  - Passive Reconnaissance: gathering information without noise
    ex) WHOIS and DNS databases. 
     > Google Dorking: using search engines to reveal sensitive information and confidential files.
  - Active Reconnaissance: gathering information that require some form of interatiction with the target organisation.
    ex) network port scanning, physics reconnaissance
    *Countermeasure: minimising public information exposure.*
    
## 2) Weaponisation
  creates a payload tailored to exploit the discovered weaknesses. 
  Exploit kit: an automated platform containing various exploits for various vulnerabilities.
  > Obfuscation: a technique to evade detection by making it challengin to analyse the malicious code.
  > Macro: a buil-in feature that makes creating a malicious MS Office document possible.
    *Countermeasure: User training, disabling any unnecessary features, uninstalling unnecessary software, removing unnecessary browser plugins, disabling macros in Office documents*

## 3) Delivery
  - Phishing emails
  - Spear phishin emails
  - Malicious web links
  - File-sharing platforms
  - Malvertising
  - SMS Phishing (Smishing)
  - Social engineering
  - Physical means of delivery
  *Countermeasure: email and web filtering, Web applicaiton firewalls(WAFs), network monitoring, patch management*

## 4) Exploitation
- zero-day exploit: an exploit that is made available before the vendor becomes aware that a vulnerability exists in their product
- the most straightforward approach: targeting a password-based authentication system.
    *Countermeasure: multi-factor authentication(MFA), Intrusion Prevention Systems(IPSs), Web Application Firewalls(WAFs)*

## 5) Installation
  - creating scheduled tasks in MS Windows or setting a cron job in Linux systems
  to modify startup scripts or configuration files. 
  Install a new service in Windows or a daemon in Linux systems

  leads to installing malware, creating backdoors, or installing rootkits, Windows tools and binaries a.k.a living-off-the land binaries(LOLBins)
  Web Shell: a small script written in a programmin language that is supported by the exploited server
  (Running a web shell over a standard protocol such as HTTPS will ensure they can log in to their target system while camouflaging their activity within HTTPS traffic)
    *Countermeasure: monitor new processes and services, endpoint detection and response(EDR) allows monitoring endpoints for suspicious activities,application allowlisting prevents the execution of unauthorised or malicious software by allowing only approved application to run* 


## 6) Command and Control(C2)

C2 Infrastructure.
common application layer protocols such as HTTP, HTTPS, DNS, and SMTP for C2 communication. 
encrypted channels such as HTTPs
DNS tunnelling.
encoding data within DNS requests. 
- commonly used media platforms: X direct messages, cloud services like Dropbox and Google Docs for data exfiltration.
  DGA. 
  Fast Flux
*Countermeasures: IDS, IPS watch for unusual traffic patterns and volumes and connections to known malicious IP addresses.*
> DNS tunnelling: tactic where data is hidden withiin DNS queries
> HTTPS: protocol the attacker use to smuggle his data as encrypted web traffic









