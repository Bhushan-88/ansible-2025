# ansible-2025
## Ansible is an open-source automation tool used for: Configuration Management: Automatically setting up and maintaining systems (e.g., installing packages, editing config files).

Setting up servers
Installing software
Managing configurations
Deploying applications


## Instead of doing these tasks manually (like clicking through screens or typing commands repeatedly), you write simple instructions once, and Ansible does them for you on any number of computers.

## Ansible primarily uses SSH (Port 22 by default) for communication with Linux/Unix hosts and WinRM (Ports 5985/5986) for Windows hosts.

## The "Why" - Why Use Ansible?
1. No More Repetitive Manual Work

Example: Instead of manually installing WordPress on 100 servers (takes days), Ansible does it in minutes with one command.
2. Consistency
Every server gets set up exactly the same way - no human mistakes or forgotten steps.
3. It's Like Recipe Books for Computers
You write "recipes" (called playbooks) that anyone can use, ensuring everyone follows the same process.
4. Free & Popular
Open-source with huge community support.
## create own ansible configuration file 
```bash
ansible-config init --disabled > ansible.cfg
```
Highest--> ANSIBLE_CONFIG=/path/to/custom.cfg-->Project-specific, CI/CD environments
High-->	./ansible.cfg -->Most common - per-project configurations
Medium--> ~/.ansible.cfg-->User-specific defaults
Lowest--> /etc/ansible/ansible.cfg-->System-wide defaults

```bash
root@ubuntu:~# mkdir /etc/ansible
root@ubuntu:~# mv ansible.cfg /etc/ansible/
root@ubuntu:~# touch /etc/ansible/hosts
root@ubuntu:~# cat > /root/hosts
192.168.1.11
root@ubuntu:~# ansible -i hosts all -u ansible --private-key=./id_rsa -m ping # for ping connected webservers
root@ubuntu:~/ansible-2025# ansible-playbook -u ansibe --private-key=./id_ed25519 my-first-playbook.yaml ORR 
root@ubuntu:~# ansible-playbook my-first-playbook.yaml
```
## what is ansible variables?
Variables = Placeholders for values that make your playbooks dynamic and reusable.

1st-priority-->CLI Variable
2st-priority-->Local Variable
3st-priority-->File Variable
4st-priority-->Promt Variable
5st-priority-->Global Variable
6st-priority-->Hosts Variable


```bash
root@ubuntu:~/ansible-2025# ansible-playbook -e url=cli.example.com variable.yaml
```

## Ansible Facts Gathering
Facts = Automatic discovery of system information
Ansible collects details about your servers automatically before running tasks.

```bash
ansible -i hosts all -m setup
```

## Register
register is used to store the output of a task in a variable, so that you can use that output in later tasks (for conditions, debugging, or logic).

## Condition
A condition controls whether a task runs or not.
In Ansible, conditions are written using the when keyword.

“Run this task only if the condition is true.”
ex:-when: ansible_os_family == "Debian"

## Privilege escalation
In Ansible, privilege escalation is called become.

Int Quetion: Privileges are permissions assigned to users or processes that determine what actions they can perform on a system. Administrative tasks require elevated privileges.

## Loop
Loops = Repeat a task multiple times with different values

Ansible loops allow a task to run multiple times using different values, reducing code repetition and improving automation efficiency.

## Setfact
set_fact is used to create or modify variables dynamically during playbook execution.

## Package module
The package module allows you to manage packages without worrying about the OS-specific package manager.

## Tags 
Tags = Labels for tasks that let you run only specific parts of a playbook.
```bash
9-tags.yaml

ansible-playbook 9-tags.yaml --tags "setup,install" #Run install OR setup tasks
ansible-playbook 9-tags.yaml --skip-tags "test"  #Skip all test tasks
ansible-playbook 9-tags.yaml --tags "always"   #Force always-tagged tasks
ansible-playbook 9-tags.yaml --list-tags  #list all tags 
```

# Copy
copy = Copy files from control node to managed nodes ORR

Use copy to send files from your computer to remote servers. Add permissions, validate, and create files directly with content!

## lineinfile
lineinfile manages individual lines in configuration files without editing the entire file.

It is commonly used for:

Configuration management
Enabling/disabling settings
Small file changes

## blockinfile
blockinfile is used to insert, update, or remove a block (multiple lines) of text in a file.
What is blockinfile used for?
Answer:
It manages multi-line configuration blocks inside files in an idempotent manner.

A marker is the label Ansible uses to identify the beginning and end of a managed block inside a file.

## Roles
A role is a structured way to organize Ansible automation into reusable components.

```bash
root@ubuntu:~# ansible-galaxy init webserver
```

## Ansible Vault is used to encrypt sensitive data so it is not stored in plain text.

What problem does Vault solve?

Passwords
API keys
SSH credentials
Database secrets

Without Vault → secrets are visible in Git
With Vault → secrets are encrypted and safe