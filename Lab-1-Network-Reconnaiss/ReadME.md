Lab 1: Network Reconnaissance (Nmap & Nikto)
Objective

The objective of this lab is to refine my reconnaissance skills that are used daily by SOC Analysts. In this lab I will be setting up a target VM (Ubuntu) then utilizing the tools within Kali Linux to retrieve information about it. I will be collecting the target's information by using its IP, running an nmap scan, and a nikto scan. The results from the lab will be posted with explanations as to how I reached them and anything else needed to be specified as well.  

Skills Learned
- Network Scanning
  --Used TCP SYN scans using Nmap to identify live hosts on a network 
- Service Enumeration
  --Enumerated open ports and detected running services and their versions.
- Operating System Fingerprinting
  --Used Nmap to infer target host operating system.
- Web Vulnerability Scanning
  --Ran Nikto against web servers to identify common vulnerabilities and misconfigurations.
- Command Line Proficiency
  --Practiced using Linux terminal to execute, chain, and interpret security tool output.

Tools Used

- Nmap – for host discovery, port scanning, service enumeration, and OS fingerprinting
- Nikto – for web server vulnerability scanning and misconfiguration detection
- Linux Terminal – for command-line interface, script execution, and report generation

Step 1: Set up target VM and find the target's IP

<img width="1470" height="956" alt="Screenshot 2025-07-28 at 10 31 12 AM" src="https://github.com/user-attachments/assets/f6b8849f-59ec-4a31-bac7-e51c728c837d" />

Explanation: 
- "ip a" is a Linux tool that commands the system to retrieve its own IP ("ipconfig" on Windows) as this is the Ubuntu target

Step 2: Run Nmap Scan(s)

Vulnerability Scan

<img width="1470" height="956" alt="Screenshot 2025-07-28 at 10 30 52 AM" src="https://github.com/user-attachments/assets/284a0bb4-7c2d-4a4c-9259-ce602c7abcf1" />

Explanation: 
- "sudo" runs nmap with root privileges as its required for some actions
- "nmap" is the actual network scanning tool we're using
- "--script vuln" is telling nmap to use vulnerability detection scripts
- at the end of the command line is the Ubuntu IP (target IP) as this is what the system is scanning

TCP Scan

<img width="1470" height="956" alt="Screenshot 2025-07-28 at 10 30 21 AM" src="https://github.com/user-attachments/assets/29bc2244-7046-4374-8192-23ec4dea4e9d" />

Explanation: 
- "sudo" runs nmap with root privileges as its required for some actions
- "nmap" is the actual network scanning tool we're using
- "-sT" is the actual TCP Connect Scan that is doing a full TCP connection using the OS
- "-p 80,443" scans only for ports 80 (HTTP) and 443 (HTTPS)
- at the end of the command line is the Ubuntu IP (target IP) as this is what the system is scanning

Stealthy Scan

<img width="1470" height="956" alt="Screenshot 2025-07-28 at 10 29 07 AM" src="https://github.com/user-attachments/assets/4b0f1799-a93b-440c-9c03-9d011f875e38" />

Explanation: 
- "sudo" runs nmap with root privileges as its required for some actions
- "nmap" is the actual network scanning tool we're using
- "-Pn" skips the host scan as it fully assumes its up even if it does not ping
- "-sS" is a SYN scan that's stealthy since it only sends half open TCP connections which makes it harder for firewalls/IDS to detect this kind of activity
- "-sV" this tool tries to determine what software is running behind ports
- at the end of the command line is the Ubuntu IP (target IP) as this is what the system is scanning

Step 3: Run Nikto Scan

<img width="1470" height="956" alt="Screenshot 2025-07-28 at 10 28 53 AM" src="https://github.com/user-attachments/assets/cfd7320c-2357-4d60-9317-4beb91a722c6" />

Explanation: 
  
Before Execeution:
  - "nikto" runs the web vulknerability scanner
  - "-h" specifies the host (IP)
  - IP at end of command line is the target

Findings:
  - X-Frame-Options header is missing so the possibility of clickjacking rises
  - X-Content-Type-Options header is missing so MIME-type sniffing risk is heightened (this could lead to a Cross-Site Scripting Attack due to the browser not guessing the correct content file type)
  - The Apache/2.4.52 is outdated which can lead to potential CVE's (Common Vulnerabilities and Exposures) so the system could be vulnerable if not updated
  - ETag (Entity Tag, header used for HTTP web caching and performance that uniquely identifies the version of the file) leaks inodes (files unique ID), mtime (last modified timestamp), and the file size







