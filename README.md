# Ansible-Config-mgt
## ANSIBLE
### STEP 1: INSTALLING AND CONFIGURING ANSIBLE ON EC2 INSTANCE
#### First, Jenkins has been installed in the Ec2 instance and a new repository named ansible-config-mgt was also created on github
#### To install Ansible
```
sudo apt update
sudo apt install ansible
```
<img width="502" alt="apt update" src="https://user-images.githubusercontent.com/112771723/195700517-153e3ea4-9b5e-4e7a-85de-6784b56609f0.png">
<img width="494" alt="ansible installed" src="https://user-images.githubusercontent.com/112771723/195699986-02cd750b-d9e1-4f0f-96d0-cbffb9521133.png">

#### Checking the ansible version `ansible --version`
<img width="493" alt="ansible version" src="https://user-images.githubusercontent.com/112771723/195700403-012b9563-2161-488f-842b-474737d987d7.png">

#### Jenkins build job was configured to save the repository content every time changes were made, also a freestyle project named "ansible" was created in Jenkins to point to the ‘ansible-config-mgt’ repository.
#### Webhook was configured in GitHub and to trigger ansible build and Post-build job was also configured in Jenkins

#### The ansible-config-mgt repository was clone down to the Jenkins-Ansible instance
```
git clone <ansible-config-mgt repo link>
```
<img width="488" alt="git clone" src="https://user-images.githubusercontent.com/112771723/195705953-6a13c386-e476-4a9a-8789-ae7b2e390708.png">

### STEP 2: PREPARING DEVELOPMENT ENVIRONMENT USING VISUAL STUDIO CODE
#### In the ansible-config-mgt github repository, a new branch named Prj11 was created, which was used for development of a new feature.
##### Command: `git checkout -b Prj11`
#### Two directories/folders Playbooks and Inventory were created. Playbook was used to store all playbook files and Inventory folder was used to keep the host organised. Within the playbooks folder, common.yml file was created for the playbook. 
#### Within the inventory folder, four files were created. They are dev.yml, staging.yml, uat.yml and prod.yml
<img width="212" alt="inventory created" src="https://user-images.githubusercontent.com/112771723/195707417-08f45ae5-1bed-4f9b-9cc9-ac2c251f31ee.png">

#### Since Ansible uses TCP port 22 by default, which means it needs to ssh into target servers from Jenkins-Ansible host. For this, the ssh-agent concept was implement
##### Commands:
```
eval `ssh-agent -s`
ssh-add <path-to-private-key>
ssh-add -l
ssh -A ubuntu@public-ip
```
<img width="446" alt="ssh add use this" src="https://user-images.githubusercontent.com/112771723/195710186-c87e00f6-543e-4fc5-85bf-ff13f193f3b3.png">

#### The inventory/dev.yml file was updated with the below code
```
[nfs]
<NFS-Server-Private-IP-Address> ansible_ssh_user='ec2-user'

[webservers]
<Web-Server1-Private-IP-Address> ansible_ssh_user='ec2-user'
<Web-Server2-Private-IP-Address> ansible_ssh_user='ec2-user'

[db]
<Database-Private-IP-Address> ansible_ssh_user='ec2-user' 

[lb]
<Load-Balancer-Private-IP-Address> ansible_ssh_user='ubuntu'
PREV
install and configure ansible on ec2 instance
```

#### The playbooks/common.yml file was also updated with the below code
```
---
- name: update web, nfs and db servers
  hosts: webservers, nfs, db
  remote_user: ec2-user
  become: yes
  become_user: root
  tasks:
    - name: ensure wireshark is at the latest version
      yum:
        name: wireshark
        state: latest

- name: update LB server
  hosts: lb
  remote_user: ubuntu
  become: yes
  become_user: root
  tasks:
    - name: Update apt repo
      apt: 
        update_cache: yes

    - name: ensure wireshark is at the latest version
      apt:
        name: wireshark
        state: latest
  ```
  











