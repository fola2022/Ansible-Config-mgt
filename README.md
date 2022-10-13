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

