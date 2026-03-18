+++
date = '2026-03-17T14:40:33+01:00'
draft = false
title = 'Ansible Starter Guide'
+++

## Introduction
This is a beginner taster course, I’m going to use Ansible to deploy and configure a basic web server. I’ll cover the core concepts and we should understand how it works and its place in a DevOps toolbox.

Pros:
- Easy to read
- Uses SSH rather than an Agent ()
- quick to deploy consistent configuration across hundreds of linux servers

Cons:
- Limited Windows support - (can’t install directly but can with WSL2)
- Being procedural, can cause errors in very large (thousands) or complex infrastructure (dynamic micro servers).

Use-cases
- Solving your own problems

And this is worth highlighting that Ansible is a great tool to solve a difficult problem in an environment you manage. It ensures servers / virtual machines are in a desired, consistent state. If there is an app that needs a specific version or data needs to be collected in a certain flow. It automates the end-to-end process of deploying applications, including copying files, installing dependencies, and restarting services in a repeatable manner.
Install Ansible
First, we install Ansible on a machine. To avoid clashing configurations, I will be using a fresh Ubuntu desktop VM. These steps are possible to run on MacOS locally but Windows does not support, so Windows Subsystem for Linux is required. I won’t cover Mac and Windows here.

Ubuntu/Debian:
sudo apt update && apt install ansible
Then verify it with:
ansible --version
Seeing a version number means it is ready. This machine now becomes our control node — the place from which we define and push configuration.

## Points to Clarify
Before moving further, let's clarify.

Agentless
Deployed agents have their own pros and cons but without needing to deploy an agent, SSH is widely integrated into Linux distributions. SSH needs to be enabled and allowed - firewall rules can lock down SSH protocol or local ports. This approach lowers the friction to achieve the task at hand.

Declarative
The Declarative part took me a while to conceptualise, in the YAML we write the desired state to get to and Ansible drives - we don’t bring a map with directions. This lowers the barrier to entry but does raise the barrier to master Ansible.

Versatility
It can handle configuration management, application deployment, and infrastructure provisioning across servers, networks, and clouds. Getting network devices to pass compliance checks is a specific use-case but easily handled by Ansible.


For this guide, we’ll use localhost as our target.

## Inventory & First Command

Create a workspace:
mkdir ansible-start
cd ansible-start

Create an inventory file:
nano inventory.ini

Set the target as the local host:
[local]
localhost ansible_connection=local

Test it:
ansible all -i inventory.ini -m ping

Which should return:
"ping": "pong"

This confirms Ansible can communicate with our defined host. Local host in this case but it is the fist hurdle.

Now a useful diagnoses command:
ansible all -i inventory.ini -m command -a "uptime"

Hurray, this proves we can query the target and can move on to more.


##First Playbook

Create a playbook:
nano install_nginx.yml
YAML is indentation (spaces) dependent, always indent by factor of two spaces for new lines.
Paste or type in:

---
- name: Install and start Nginx
  hosts: local
  become: yes

  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present
        update_cache: yes

    - name: Ensure Nginx is running
      service:
        name: nginx
        state: started
        enabled: yes


To run it (make sure you’re in the correct directory):
ansible-playbook -i inventory.ini install_nginx.yml

What happened? Ansible gets Nginx installed, started, and enabled. If we run it again, nothing should change.

If you can’t view the target host default Nginx webpage, we can pull it with:
curl http://localhost

Terminal should output the default Nginx page.

## Dynamic Variables
To improve the playbook, replace hardcoded values with variables.
Create another playbook:
nano install_webserver.yml

Paste in:

---
- name: Install web server
  hosts: local
  become: yes
  vars:
    package_name: nginx

  tasks:
    - name: Install package
      apt:
        name: "{{ package_name }}"
        state: present
        update_cache: yes

By introducing package_name, it becomes reusable. If we want apache2, the same structure installs a different server. 

Variables are stated in the vars section and referenced using the double quotes, double curly braces, space name, variable name {{ var-name }}. Which is to align with the same convention from Jinja2 (j2 files).

Templates (the Real value)
Let’s customize the homepage.

Create a templates directory:
mkdir templates
nano templates/index.html.j2

Paste in:
<h1>Hello {{ ansible_hostname }}</h1>
<p>Deployed using Ansible.</p>

Now update the playbook:

---
- name: Install web server
  hosts: local
  become: yes
  vars:
    package_name: nginx

  tasks:
    - name: Install package
      apt:
        name: "{{ package_name }}"
        state: present
        update_cache: yes

    - name: Deploy custom index page
      template:
        src: templates/index.html.j2
        dest: /var/www/html/index.html

    - name: Ensure web server is running
      service:
        name: "{{ package_name }}"
        state: restarted
        enabled: yes


Run:
ansible-playbook -i inventory.ini install_webserver.yml

When we refresh the browser, the page is generated using the template variable. This is touching on the real value.

If needed, pull it with:
curl http://localhost

## Example Structure
A realistic layout looks like:

ansible-start/
│
├── inventory.ini
├── site.yml
├── roles/
│   └── web/
│       ├── tasks/main.yml
│       ├── templates/
│       └── handlers/

(tree -L 3)

From here, a next step is to target remote VMs over SSH and manage multiple hosts.

