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
