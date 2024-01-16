#############################
### Author: Yatin Gambhir
### Date: 16 January 2024
### Topic: Ansible Setup
################################

Step 1 - To install Ansible on your machine, launch two EC2 instances one with "ansible-master" & "ansible-server1" and SSH into the "ansible-master" server by opening Command Prompt and using the below commands.
ssh -i "private-key-path.pem" 'username'@'public-ip-address' #To login into the server

On successful logging in update the packages and install ansible:

sudo apt update
sudo apt install ansible 

Upon successful installation of Ansible verify it using the: 
ansible --version

Step 2 - Your ansible is successfully installed on the master node. Now we have ssh into the other server, so for that do the below steps:
 - Open the private key file in your windows and copy the content of your private key file
 - Now in the instance do "cd  ~/.ssh" where your private key file will be stored
 - Create a new file using "nano ansible_key" and copy the content of the private key and save the file
 - Give the permissions to the "~/.ssh" folder and the "ansible_key" file using "chmod 700 ~/.ssh" & "chmod 600 ~/.ssh/ansible_key"
 - Now move to the home directory using the "cd" command and try to login into the target server using "ssh -i ~/.ssh/ansible_key 'username'@'public_ip'". You will see that you are connected with the target server.
 - Logout from the target server to go to the master server

 Step 3 - Now we will use the Ansible to test the connection. Follow the below steps and create an inventory file that includes all the target servers.
  - mkdir ansible
  - nano hosts (The sample of hosts file is included in my Github repository)

Step 4 - To check whether my host file (according to the GitHub repo) is correct use the below command:
 ansible-inventory server -m ping -i inventory_file (/home/ubuntu/ansible/hosts) --private-key=ansible_ssh_private_key (~/.ssh/ansible_key)

YOU SHOULD SEE THAT THE RESULT IS SUCCESS AND OUTPUT IS 'ping':'pong'.

--OUR CONNECTION TO THE TARGET SERVER is SUCCESSFULLY CONFIGURED.--

Now we will understand the Playbook

Step 1 - I have pushed the three playbooks files where we will see the automation to "create a file", "add a user" & "install docker" on each server

YOU CAN CHECK THE PLAYBOOK FILES FOR YOUR REFERENCE

Step 2 - After creating the playbook.yaml file enter the below command

ansible-playbook 'file-name.yaml' -i /home/ubuntu/ansible/hosts --private-key=~/.ssh/ansible_key

This will do the task you have written inside your playbook file.

Step 3 - To verify if the task is performed connect with the target server and check whether the required task is performed or not.


TERMINATE THE INSTANCE AFTER TASK IS PERFORMED
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
