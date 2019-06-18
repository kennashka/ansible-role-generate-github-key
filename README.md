# ansible-role-generate-github-key
Ansible role to generate a new SSH key for Github and add it to the ssh-agent.


### Version

1.1.0

## Required: Ansible Install for Ubuntu

```bash
sudo apt-get update
sudo apt-get install software-properties-common
sudo apt-add-repository --yes --update ppa:ansible/ansible
sudo apt-get install ansible

```


## Role Installation 

```bash

ansible-galaxy install kennashka.ansible_role_generate_github_key
```

## Configure Hosts File (Optional Way to Give Permissions for Accessing Server)

1. Replace (12.345.678.90) with your target server ip/domain address in hosts file 
2. Add the file location to ssh pem key in hosts file (ex. ansible_ssh_private_key_file= directory/location/to/your/pem/key/file.pem)
3. Another option way is to generate IAM role for ec2 then use boto for accessing server


## Configure "tasks/generate.yml" File:
 Replace File Variables With Targeted Host Machine, Default User (root permission is needed to run certain tasks).
 
```yml
- hosts: addyourhost
  remote_user: ubuntu
  become: yes
```
```yml
  vars:
    github_email: "mail@gmail.com"
    default_file_location: "\n" 
    secure_passphrase: "yourpassphrase"
 ```   
## Steps for execution:

[x] Run
```bash
ssh-keygen -t rsa -b 4096 -C "youremail@gmail.com"
```
[x] Type in a file location and password (ansible will save to default location)

[x] Start the ssh-agent in the background.

```bash
eval `ssh-agent`
```

[x] ssh-add
```bash
ssh-add ~/.ssh/id_rsa
```

[ ] Copy ssh key gen public key and add SSH Key to your Github account (this has to be done manually for now, update coming soon!)
[Follow the Instructions Here:](https://help.github.com/en/articles/adding-a-new-ssh-key-to-your-github-account)


```bash
vim /root/.ssh/id_rsa.pub

```

## Run To Start 
```bash
ansible-playbook -i ./hosts tasks/generate.yml
```
