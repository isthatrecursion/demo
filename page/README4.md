To automate software provisioning and configuration using Ansible.
2. Procedure
Step 1: Check and install Ansible
First, check whether Ansible is installed.

ansible --version


If Ansible is not installed, execute:

sudo apt update
sudo apt install ansible -y


After installation, verify:

ansible --version


Information: Checks the Ansible version and installs it on Ubuntu only if required.
Step 2: Create a project folder

mkdir ansible-lab
cd ansible-lab


Information: Creates a folder named ansible-lab and enters it.
Step 3: Create an inventory file

nano inventory


Write the following code:

localhost ansible_connection=local


Save the file by pressing Ctrl + O, Enter, and Ctrl + X.

Information: The inventory file specifies the host on which Ansible will perform tasks. Here, the host is the local machine.
Step 4: Test Ansible

ansible all -i inventory -m ping


Information: Tests the connection to the local machine.

Expected output includes:
localhost | SUCCESS => {
    "changed": false,
    "ping": "pong"
}


Step 5: Create an Ansible playbook

nano install-nginx.yml


Write the following code:

---
- name: Install Nginx
  hosts: localhost
  connection: local
  become: yes

  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present


Save the file using Ctrl + O, Enter, and Ctrl + X.

Information: Creates a playbook that automates the installation of Nginx on Ubuntu.
Step 6: Run the playbook

ansible-playbook -i inventory install-nginx.yml


Information: Executes the playbook and installs Nginx. Enter your password if prompted.
Step 7: Check the Nginx service

systemctl status nginx


Information: Checks whether the Nginx service is running. Press q to exit the status screen.
Step 8: Open the browser

Open your web browser and enter:

http://localhost

Information: If Nginx is running correctly, its default welcome page should appear.