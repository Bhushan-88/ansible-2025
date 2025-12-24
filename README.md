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