# Install Ansible
    sudo amazon-linux-extras install ansible2  # to check the installation; ansible --version

# Add the public or private IPs of the remote systems to be configured in to 'hosts' file located in /etc/ansible
    sudo su
    cd /etc/ansible
    ls
    vim hosts

    [webservers]
    node1 ansible_host=<node1_ip> ansible_user=ec2-user
    node2 ansible_host=<node2_ip> ansible_user=ec2-user

    [all:vars]
    ansible_ssh_private_key_file=/home/ec2-user/<pem file>  # you need to copy your pem file to /home/ec2-user

## Ansible Ad-hoc commands

# To confirm that all our hosts are located by Ansible
    ansible all --list-hosts
    ansible webservers --list-hosts

# To make sure that all our hosts are reachable
    ansible all -m ping
    ansible webservers -m ping   # ping only webserver group
    ansible node1 -m ping   # ping only node1

"ansible-doc <module_name>" command is used for seeing the explanation and examples of a specific module.
    ansible-doc ping

# Ping all the hosts
    ansible all -m ping -o   #  -m: module,  -o: oneline, show the result in one line

# To get rid of the warning about the deprication of the usage of Python2, add the following lines to /etc/ansible/ansible.cfg file
    [defaults]
    interpreter_python=auto_silent

    # uncomment this to disable SSH key host checking
    host_key_checking = False

# To run a playbook
    ansible-playbook playbook1.yaml

# Create encypted variables using "ansible-vault" command
    ansible-vault create secret.yml

# Run a playbook with vault:
    ansible-playbook --ask-vault-pass create-user.yml

# Using Ansible Roles from Ansible Galaxy
    ansible-galaxy install geerlingguy.nginx