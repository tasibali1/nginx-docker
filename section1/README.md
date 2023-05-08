# Offline Screening Evaluation

## Section 1): Test your R&D skills:
1. Explain the following types of DDoS attacks? Explain the cause, effect, and mitigation for these attacks:
- a. CC (Challenge Collapsar) attack.
- b. SYN Flood attack.
- c. SSL Attack

Note: Format of the answer should be divided into 4 sections as follows: 
- Cause: (To explain What is the cause of attack)
- Identify: (To explain How will you identify this attack.)
- Effect: (To explain What is the effect of this attack.)
- Mitigation: ( To explain How will you mitigate this.)

## Answer:
1. a. CC (Challenge Collapsar) attack:
- Cause: CC (Challenge Collapsar) attack is a type of DDoS attack where the attacker floods the target server with a high volume of HTTP or HTTPS requests that require computational resources to process. These requests often involve computationally expensive operations, such as solving complex mathematical challenges or CAPTCHAs, which consume the server's CPU power and memory.
- Identify: CC attacks can be identified by monitoring the server's incoming traffic patterns. A sudden spike in HTTP/HTTPS requests, especially those involving resource-intensive computations, is a strong indication of a CC attack.
- Effect: The effect of a CC attack is the exhaustion of server resources. The server becomes overwhelmed with the flood of requests, causing a significant increase in response times or even complete unavailability. Legitimate users may experience service disruptions, and the server's performance may degrade or crash.
- Mitigation: Mitigating CC attacks involves implementing various strategies such as rate limiting, CAPTCHA challenges, and traffic filtering. Some specific mitigation techniques include:
  - Implementing CAPTCHA or similar challenge-response mechanisms to ensure legitimate users can access the server while filtering out bot-generated requests.
  - Deploying anti-DDoS solutions that can detect and block CC attacks based on traffic patterns, IP reputation, or anomaly detection algorithms.
  - Scaling server resources to handle increased traffic during attacks, either through load balancing or cloud-based infrastructure.

1. b. SYN Flood attack:
- Cause: A SYN Flood attack exploits the TCP three-way handshake process. The attacker sends a flood of TCP SYN packets with spoofed source IP addresses, causing the targeted server to allocate resources for incomplete connections that are never completed.
- Identify: SYN Flood attacks can be identified by monitoring network traffic for an unusually high number of SYN packets with no corresponding ACK responses. Network monitoring tools or intrusion detection systems can raise alerts when SYN Flood patterns are detected.
- Effect: The effect of a SYN Flood attack is the exhaustion of the server's resources, particularly its connection state table. The server becomes overwhelmed with half-open connections, consuming memory and processing power. As a result, legitimate clients may experience delays or failure to establish connections with the server.
- Mitigation: Mitigating SYN Flood attacks involves implementing various techniques, including:
  - Implementing SYN cookies, a technique that allows the server to validate the legitimacy of connection requests without reserving resources for half-open connections.
  - Configuring firewalls or network devices to detect and drop spoofed or excessive SYN packets.
  - Using rate-limiting mechanisms to limit the number of incoming connection requests per second from a single IP address.
  - Deploying DDoS mitigation solutions or services that can detect and filter out SYN Flood attacks based on traffic patterns or anomaly detection algorithms.

1. c. SSL Attack:
- Cause: SSL (Secure Sockets Layer) attacks exploit vulnerabilities or weaknesses in the SSL/TLS protocol or its implementation. These attacks can include various techniques, such as exploiting weak cipher suites, SSL renegotiation vulnerabilities, or certificate-related weaknesses.
- Identify: SSL attacks can be identified through monitoring and analyzing SSL/TLS handshake exchanges, examining certificate chains for anomalies or expired certificates, and using vulnerability scanning tools to identify known SSL vulnerabilities.
- Effect: The effect of an SSL attack depends on the specific vulnerability being exploited. Possible effects include:
  - Man-in-the-Middle (MitM) attacks, where an attacker intercepts and decrypts encrypted communication between two parties, allowing them to eavesdrop or tamper with the data.
  - Information disclosure or data leakage if SSL vulnerabilities allow unauthorized access to sensitive information.
  - Denial-of-Service (DoS) attacks that target SSL/TLS services, this can result in unavailability of secure services and compromise the overall performance and functionality of the system.
- Mitigation: To mitigate SSL attacks, several measures can be implemented:
  - Implement rate limiting: Enforce rate limiting mechanisms to prevent excessive SSL/TLS handshakes from a single source. This helps mitigate attacks that rely on overwhelming the server with a large number of handshakes.
  - Employ SSL/TLS termination proxies: Deploy SSL/TLS termination proxies or load balancers to offload the SSL/TLS encryption and decryption process from backend servers. This provides better control and inspection of SSL/TLS traffic, allowing detection and mitigation of potential attacks.
  - Keep software up to date: Regularly update and patch SSL/TLS libraries and server software to address known vulnerabilities. This helps protect against attacks that exploit known weaknesses in SSL/TLS protocols.
  - Implement traffic monitoring and anomaly detection: Deploy network monitoring tools capable of detecting unusual patterns in SSL/TLS traffic. Anomaly detection mechanisms can help identify and flag potential SSL attacks for further investigation and mitigation.
  - Use hardware acceleration and load balancing: Leverage hardware acceleration and load balancing techniques to distribute SSL/TLS processing across multiple servers or specialized hardware devices. This distributes the computational load and enhances resilience against SSL attacks.
  - Enable rate limiting and connection timeouts: Configure rate limiting and connection timeouts on SSL/TLS services to limit the impact of potential SSL attacks. By setting reasonable limits on the number of connections and imposing timeouts for idle connections, resources can be managed effectively and potential attacks mitigated.
  - Deploy intrusion detection/prevention systems (IDS/IPS): Implement IDS/IPS systems to detect and prevent SSL attacks by analyzing network traffic for suspicious patterns or known attack signatures. These systems provide an additional layer of security to identify and block SSL attacks in real-time.
