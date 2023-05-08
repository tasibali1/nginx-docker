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



## Section 2): Test check system administration skills:

2. On an Ubuntu system install Nginx 1.23.1 from a source file (Not using APT) and create a small test infrastructure on your virtual environment to perform a load balancing of a site example.com using Nginx. Share the steps and screenshots of the configuration and the result identifying the load has been distributed among backend servers.

## Answer:
To install Nginx 1.23.1 from a source file on an Ubuntu system and configure load balancing for the site example.com, follow these steps:

1. Download the Nginx source file:
   - Visit the Nginx download page (https://nginx.org/en/download.html) and find the link to download the source file for version 1.23.1.
   - Use a tool like `wget` to download the source file. For example:
     ```
     wget https://nginx.org/download/nginx-1.23.1.tar.gz
     ```

2. Extract the source file:
   - Use the `tar` command to extract the downloaded source file. For example:
     ```
     tar -xzvf nginx-1.23.1.tar.gz
     ```

3. Install build dependencies:
   - Install the necessary build dependencies by running the following commands:
     ```
     sudo apt-get update
     sudo apt-get install build-essential
     ```

4. Configure and build Nginx:
   - Change into the extracted Nginx source directory:
     ```
     cd nginx-1.23.1
     ```

   - Configure Nginx with the desired options. For load balancing, you need to enable the `http_upstream_module`. You can also add other modules or configure additional options as needed. Run the following command to configure Nginx:
     ```
     ./configure --with-http_upstream_module
     ```

   - Build Nginx by running the following command:
     ```
     make
     ```

   - Once the build process completes, install Nginx by running:
     ```
     sudo make install
     ```

5. Configure load balancing in Nginx:
   - Create a new Nginx configuration file for the load balancing:
     ```
     sudo nano /usr/local/nginx/conf/nginx.conf
     ```

   - Inside the `http` block, add the following configuration to define the upstream servers and enable load balancing:
     ```nginx
        upstream backend {
            server backend1.example.com;
            server backend2.example.com;
            # Add more backend servers if needed
        }

        server {
            listen 80;
            server_name example.com;

            location / {
            proxy_pass http://backend;
            }
        }
     ```

   - Save the configuration file and exit the text editor.

6. Start Nginx:
   - Start Nginx using the following command:
     ```
     sudo /usr/local/nginx/sbin/nginx
     ```

7. Verify load balancing:
   - Ensure that the backend servers (backend1.example.com, backend2.example.com, etc.) are running and accessible.

   - Open a web browser and visit http://example.com. Refresh the page multiple times.
   
   - Use the appropriate tools to monitor the backend servers and observe the distribution of incoming requests.

   - If load balancing is working correctly, you should see that the requests are distributed among the backend servers.

This setup assumes that you have already configured the DNS or hosts file to map example.com to the IP address of the Ubuntu system running Nginx.

## Dockerized Way:

To create a Docker container of Nginx 1.23.1 from source on Ubuntu, you can use a Dockerfile to define the build steps and configuration. Here are the steps:

1. Create a directory for your Docker build context and navigate to it:
   ```bash
   mkdir nginx-docker
   cd nginx-docker
   ```

2. Create a file named `Dockerfile` using a text editor:
   ```Dockerfile
   # Use Ubuntu as the base image
   FROM ubuntu:latest
   
   # Install build dependencies
   RUN apt-get update && \
       apt-get install -y build-essential curl tar && \
       rm -rf /var/lib/apt/lists/*
   
   # Set the Nginx version
   ENV NGINX_VERSION=1.23.1
   
   # Download and extract Nginx source
   RUN curl -LO https://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz && \
       tar -xzf nginx-${NGINX_VERSION}.tar.gz && \
       rm nginx-${NGINX_VERSION}.tar.gz
   
   # Build Nginx from source
   RUN cd nginx-${NGINX_VERSION} && \
       ./configure && \
       make && \
       make install
   
   # Expose port 80
   EXPOSE 80
   
   # Start Nginx when the container is run
   CMD ["nginx", "-g", "daemon off;"]
   ```

3. Build the Docker image:
   ```bash
   docker build -t nginx-from-source .
   ```

4. Run the Docker container:
   ```bash
   docker run -d -p 80:80 nginx-from-source
   ```

5. Verify the container is running:
   ```bash
   docker ps
   ```

Now, you have a Docker container based on Ubuntu with `Nginx 1.23.1` installed from source. It is listening on port 80 inside the container, which is mapped to port 80 on the host system.
The Docker container will work the same way as the manual installation, distributing the load among the backend servers.

To test the load balancing setup with Nginx using Docker, you can create a `docker-compose.yml` file with multiple backend server containers and an Nginx container configured for load balancing. Here's an example of a `docker-compose.yml` file:

```yaml
version: '3'

services:
  nginx:
    image: nginx-from-source:latest
    ports:
      - 80:80
    volumes:
      - ./nginx.conf:/etc/nginx/conf.d/default.conf
    depends_on:
      - backend1
      - backend2

  backend1:
    image: containous/whoami
    expose:
      - 80
    command: --port=80

  backend2:
    image: containous/whoami
    expose:
      - 80
    command: --port=80
```

Make sure you have a `nginx.conf` file in the same directory as the `docker-compose.yml` file. This file will be mounted into the Nginx container to provide the load balancing configuration.

Here's an example `nginx.conf` file for load balancing:

```conf
upstream backend {
    server backend1:80;
    server backend2:80;
    # Add more backend servers if needed
  }

server {
    listen 80;
    server_name example.com;

    location / {
      proxy_pass http://backend;
    }
  }
```

In this configuration, the `upstream` block defines the backend servers, and the `server` block specifies the load balancing configuration. Ensure that the `server_name` matches the domain you want to test.

To test the setup:

1. Save the `docker-compose.yml` and `nginx.conf` files in the same directory.
2. Open a terminal or command prompt and navigate to the directory containing the files.
3. Run the following command to start the containers:
   ```
   docker-compose up
   ```
4. Wait for the containers to start. You should see output indicating the containers are running.
5. Open a web browser and visit http://example.com. Refresh the page multiple times, you will see IP of the containers switch after each refresh.
6. Observe the load balancing by monitoring the backend containers' logs or using appropriate tools to track the distribution of incoming requests.


## Section 3): To check automation skills:

3. Write an ansible role to install Kong Gateway from source in an ubuntuserver, the script should include:
a. Building kong gateway in host ( Note: do not use apt or dpkg to install kong. Should use only source 2.8 latest)
b. Setting up the auto startup script.
c. Submit your github url.

## Answer:

To create an Ansible role for installing Kong Gateway from source on an Ubuntu server, follow these steps:

1. Create a directory for your Ansible role:
   ```bash
   mkdir kong-gateway-role
   cd kong-gateway-role
   ```

2. Create a file named `kong-gateway-role.yml` using a text editor:
   ```yaml
   ---
   - name: Install Kong Gateway
     hosts: all
     become: true
   
     tasks:
       - name: Install dependencies
         apt:
           name: "{{ item }}"
           state: present
         with_items:
           - unzip
           - libpcre3-dev
           - libssl-dev
           - perl
   
       - name: Download Kong Gateway source
         get_url:
           url: https://github.com/Kong/kong/archive/2.8.0.tar.gz
           dest: /tmp/kong.tar.gz
   
       - name: Extract Kong Gateway source
         unarchive:
           src: /tmp/kong.tar.gz
           dest: /tmp
           remote_src: true
   
       - name: Build Kong Gateway from source
         shell: |
           cd /tmp/kong-2.8.0
           make install
   
       - name: Set up auto startup script
         copy:
           content: |
             #!/bin/bash
             /usr/local/bin/kong start
           dest: /etc/init.d/kong
           mode: '0755'
   
       - name: Enable Kong Gateway service
         service:
           name: kong
           enabled: yes
           state: started
   ```

3. Save the file and exit the text editor.

4. Create a directory named `roles` inside the `kong-gateway-role` directory:
   ```bash
   mkdir roles
   ```

5. Create a directory named `kong` inside the `roles` directory:
   ```bash
   mkdir roles/kong
   ```

6. Move the `kong-gateway-role.yml` file into the `roles/kong` directory:
   ```bash
   mv kong-gateway-role.yml roles/kong/main.yml
   ```

7. Initialize the Ansible playbook:
   ```bash
   ansible-playbook main.yml
   ```

8. Test the playbook against your Ubuntu server:
   ```bash
   ansible-playbook -i <inventory_file> main.yml
   ```

   Replace `<inventory_file>` with the path to your Ansible inventory file containing the target Ubuntu server.

9. Verify that Kong Gateway is installed and running on the Ubuntu server.
