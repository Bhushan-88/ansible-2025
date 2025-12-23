# ansible-2025
# Ansible is an open-source automation tool used for: Configuration Management: Automatically setting up and maintaining systems (e.g., installing packages, editing config files).

Setting up servers
Installing software
Managing configurations
Deploying applications
# Instead of doing these tasks manually (like clicking through screens or typing commands repeatedly), you write simple instructions once, and Ansible does them for you on any number of computers.

## Ansible primarily uses SSH (Port 22 by default) for communication with Linux/Unix hosts and WinRM (Ports 5985/5986) for Windows hosts.

# create own ansible configuration file 
ansible-config init --disabled > ansible.cfg
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
root@ubuntu:~# ansible -i hosts all -u ansible --private-key=./id_rsa -m ping
```