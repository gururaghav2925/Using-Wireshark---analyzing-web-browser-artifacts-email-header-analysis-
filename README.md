# Using-Wireshark---analyzing-web-browser-artifacts-email-header-analysis
## AIM:
To use Wireshark to analyze web browser activities and inspect email headers from captured network traffic.
## Architecture Diagram:
```mermaid
flowchart TD
    A[User System] --> B[Web Browser]
    A --> C[Email Client]
    B --> D[Network Traffic]
    C --> D
    D --> E[Wireshark Capture Engine]
    E --> F[Protocol Decoders HTTP SMTP IMAP POP]
    F --> G[Browser Artifacts URLs Cookies Auth]
    F --> H[Email Headers Source IP Server Timestamps]
    G --> I[Findings and Reports]
    H --> I
```
## DESIGN STEPS:
### Step 1:
- Install Wireshark and ensure correct network adapter selection.
- Enable packet capturing for your active interface (Wi-Fi/Ethernet).

### Step 2:
**Web Browser Artifact Analysis**
- Open a browser and visit websites with login forms (use dummy credentials).
- In Wireshark, filter traffic with:
    - ```http``` for normal HTTP requests
    - ```http.cookie``` for cookies
    - ```http.authbasic``` for basic authentication
- Identify:
    - URLs visited
    - GET/POST requests
    - Cookies & session IDs
    - Credentials (if plaintext HTTP is used)
### Step 3:
- Capture email traffic by sending/receiving emails (dummy mail server or provided PCAP).
- Use filters:
    - ```smtp``` (Simple Mail Transfer Protocol)
    - ```pop``` / ```imap``` (for received mail)
- Inspect email headers:
    - Source IP
    - Mail server hostname
    - Timestamps
    - Possible forged headers
## PROGRAM:
```mermaid
flowchart TD
    A[Start Wireshark Capture] --> B[Generate Traffic: Web Browsing & Emails]
    B --> C[Apply Protocol Filters: HTTP/SMTP/IMAP/POP]
    C --> D[Extract Browser Artifacts: URLs, Cookies, Credentials]
    C --> E[Analyze Email Headers: Source, Server, Metadata]
    D --> F[Save Findings]
    E --> F[Save Findings]
    F --> G[Generate Digital Forensic Report]
```

## A. Capturing Traffic in Wireshark

1. Open Wireshark and start capturing on the active interface (Wi-
Fi/Ethernet).


<img width="1920" height="1080" alt="Screenshot 2025-09-27 234621" src="https://github.com/user-attachments/assets/2f654fe3-d883-4d0e-889a-01d80527cbbf" />


2. Perform activities like opening a website or sending an email through a
client (e.g., Gmail via browser or Thunderbird).


<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/1c285403-5835-4891-b7ed-0a4315944146" />


4. Stop the capture once done.


## B. Analyzing Web Browser Artifacts
1. Apply filters like: http, tcp.port == 443 (for HTTPS), or dns to isolate
browser traffic.


<img width="1920" height="1080" alt="Screenshot 2025-09-28 000031" src="https://github.com/user-attachments/assets/cafacde3-45c4-40b0-897f-e830c514e74b" />


3. Inspect HTTP GET/POST requests:
o Look for URLs, hostnames, user agents, and cookies in the HTTP
headers.
o Follow TCP Stream to reconstruct page request flow:
▪ Right-click a packet → Follow → TCP Stream.


<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b93f033d-4c26-4ea7-b40d-e8b30730213f" />


Analyze DNS Queries:
o Filter: dns
o Reveal domains the browser tried to resolve.


<img width="1920" height="1080" alt="Screenshot 2025-09-28 000112" src="https://github.com/user-attachments/assets/44d652fb-9e8c-429f-bb01-834e6778e7a3" />


## C. Email Header Analysis
1. Apply relevant filters:
o For POP3: tcp.port == 110
o For SMTP: tcp.port == 25 or 587
o For IMAP: tcp.port == 143 or 993


<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/7cc806d8-a833-4178-9e27-1dd22030f82b" />


3. Locate email data:
o Look for SMTP packets to see sender/receiver email addresses.
o Use "Follow TCP Stream" to view the full email headers and body if
unencrypted.


<img width="1919" height="459" alt="Screenshot 2025-09-28 004549" src="https://github.com/user-attachments/assets/60a19f8d-a383-4002-8283-faf59ccf3514" />


5. Extract Email Header Fields:
o Analyze From, To, Subject, Date, Message-ID, and relay servers used
in sending the email.


<img width="1920" height="1080" alt="Screenshot 2025-09-28 004647" src="https://github.com/user-attachments/assets/710b51ec-efa9-495a-95d6-efc84b2fde45" />


## OUTPUT:
Captured Web Activity and Email Header Information

## RESULT:
Web browser artifacts and email headers were successfully analyzed using Wireshark.

