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
