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
