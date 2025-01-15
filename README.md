# Analyze-Network-Attacks

<h2> Scenario </h2>
You work as a security analyst for a travel agency that advertises sales and promotions on the company’s website. The employees of the company regularly access the company’s sales webpage to search for vacation packages their customers might like. 

One afternoon, you receive an automated alert from your monitoring system indicating a problem with the web server. You attempt to visit the company’s website, but you receive a connection timeout error message in your browser.

You use a packet sniffer to capture data packets in transit to and from the web server. You notice a large number of TCP SYN requests coming from an unfamiliar IP address. The web server appears to be overwhelmed by the volume of incoming traffic and is losing its ability to respond to the abnormally large number of SYN requests. You suspect the server is under attack by a malicious actor. 

You take the server offline temporarily so that the machine can recover and return to a normal operating status. You also configure the company’s firewall to block the IP address that was sending the abnormal number of SYN requests. You know that your IP blocking solution won’t last long, as an attacker can spoof other IP addresses to get around this block. You need to alert your manager about this problem quickly and discuss the next steps to stop this attacker and prevent this problem from happening again. You will need to be prepared to tell your boss about the type of attack you discovered and how it was affecting the web server and employees.

<h2> Cybersecurity Incident Report </h2>

 <h2>Section 1: Identify the Type of Attack </h2> 

## Attack Type: ##
The network intrusion observed in this scenario is a TCP SYN Flood Attack, a type of Denial-of-Service (DoS) attack.

- Symptoms:
A large volume of TCP SYN requests is directed to the web server from an unfamiliar IP address.
The server becomes overwhelmed, unable to handle legitimate requests, and results in connection timeout errors for website visitors.

- How It Impacts Network Performance:
The server allocates resources for each incoming SYN request as part of the TCP three-way handshake process. When these requests are excessive and incomplete, the server's resources become exhausted, leading to its inability to process further requests.
This effectively renders the website inaccessible to legitimate users.

<h2> Section 2: Explain How the Attack Causes Website Malfunction </h2>

**TCP Three-Way Handshake Steps**:
  - *Step 1 (SYN)*: The client sends a TCP SYN packet to the server, requesting to   establish a connection.
  - *Step 2 (SYN-ACK)*: The server responds with a SYN-ACK packet, acknowledging the request and confirming readiness.
  - *Step 3 (ACK)*: The client replies with an ACK packet, completing the handshake.

**Malicious Actor’s Behavior**:
The attacker sends an abnormally large number of SYN packets but does not complete the handshake by sending ACK packets. This leaves the server waiting for acknowledgments that will never arrive, consuming resources unnecessarily.

**Logs Analysis**:
The logs show repetitive SYN requests from multiple IP addresses, indicating the possibility of IP address spoofing to avoid detection and bypass basic IP blocking mechanisms.
The server responds with SYN-ACK packets but receives no ACK packets, leading to resource exhaustion and degraded server performance.
Potential Consequences of the Attack

**Business Disruption**:
The website is rendered inaccessible, preventing employees from assisting customers and impacting customer satisfaction.

**Reputation Damage**:
Persistent downtime may result in loss of trust from customers.

**Operational Costs**:
Resources are consumed for mitigating the attack, including manpower and technology costs.

<h2> Recommendations for Mitigation and Prevention</h2>

## Immediate Actions: ##
Take the server offline temporarily to recover and stop ongoing attack traffic.
Block malicious IPs using firewall rules and monitor traffic for new patterns of suspicious behavior.

## Long-Term Solutions: ##
  
- **Implement SYN Cookies**: Use SYN cookies to prevent resource exhaustion by verifying incoming SYN requests without allocating server resources until the handshake is complete.
- **Rate Limiting**: Configure rate limits on SYN packets to prevent overwhelming the server.
- **Deploy a Web Application Firewall (WAF)**: A WAF can help detect and filter malicious traffic.
- **Use a Content Delivery Network (CDN)**: A CDN can distribute traffic across multiple servers, reducing the load on the primary server.
- **Traffic Anomaly Detection**: Implement monitoring tools that use machine learning to identify and mitigate anomalous traffic patterns in real time.

<h2> Conclusion </h2>
This TCP SYN Flood Attack exploited the server's resource allocation process to overwhelm it and disrupt normal operations. Immediate actions have stabilized the server, but implementing long-term solutions such as SYN cookies and traffic filtering are critical to prevent future attacks. 

<h2> TCP LOG FILE:</h2>
[ Wireshark TCP_HTTP log - TCP]( https://docs.google.com/spreadsheets/d/1enpRzrIao3J2Lp2tOI0hmu1Cu7D7CjLGhFAiTiR9J64/edit?gid=218501934#gid=218501934 )
