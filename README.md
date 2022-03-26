# Project-1-Elk-Stack
This include all the files and images that explain and show what happened in the process of doing the project.

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Diagrams/networking.png](https://github.com/nabouneama/Project-1-Elk-Stack/blob/main/Diagrams/networking.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the filebeat-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

  - [filebeat-playbook.yml](https://github.com/nabouneama/Project-1-Elk-Stack/blob/main/Ansible/roles/filebeat-playbook.yml)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
- Load balancers distributes and divide the network traffic onto many servers which help increase the capacity of the users. They protect and ensures the availability of the information if one server went down or crashed. 
- A jumpbox is a system on a network that is used to access all the information needed within a more secured machine. It is used to protect the information and limit the people who have access to the information.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- Filebeat collects and records log files and forwards them to logstach or elastic search.
- Metricbeat records metrics and statistics from teh system and services on the server.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function                                  | IP Address | Operating System |
|----------|----------------------------------------------------------|------------|------------------|
| Jump Box | Gateway                                                  | 10.0.0.4   | Linux            |
| WEB 1    | Accessing the cloud & accepts requests from web browsers | 10.0.0.5   | Linux            |
| WEB 2    | Accessing the cloud & accepts requests from web browsers | 10.0.0.6   | Linux            |
| ELK vm   | Record logs from systems and applications                | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 20.106.159.198

Machines within the network can only be accessed by the jumpbox.
- The jumpbox can access all the vms (web 1, web 2, Elk vm). The private IP address of the jumpbox is 10.0.0.4 while the public IP address is 20.106.159.198.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses               |
|----------|---------------------|------------------------------------|
| Jump Box | Yes                 | 20.106.159.198                     |
| Web 1    | No                  | 10.0.0.4                           |
| Web 2    | No                  | 10.0.0.4                           |
| ELk vm   | Yes                 | 20.106.159.198, 10.0.0.5, 10.0.0.6 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Ansible is easy to use and doesn't require coding skills. 
- It also helps with the representation of IAC Infrastructure as Code.
- It makes writing complex playbooks easy and able to be reused.

The playbook implements the following tasks:
- Install docker.io
- Install python3.pip
- Install docker module
- increase the virtual memory 
      - sysctl -w vm.max_map_count-262144
- Launch the container with sebt/elk:761 image on ports
      - 5601:5601
      - 9200:9200
      - 5044:5044

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Docker_ps_output](https://github.com/nabouneama/Project-1-Elk-Stack/blob/main/Images/verifying-the-container.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat:
    - collects log files and forwards them to elastcisearch for advanced processing.
- Metricbeat:
    - collects statistics and metrics logs from the operating system and from services running on the server.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the [ansible.cfg](https://github.com/nabouneama/Project-1-Elk-Stack/blob/main/Ansible/ansible.cfg) file to /etc/ansible.
- Update the [hosts](https://github.com/nabouneama/Project-1-Elk-Stack/blob/main/Ansible/hosts) file to include the hosts and their IP addresses
  ![hosts](https://github.com/nabouneama/Project-1-Elk-Stack/blob/main/Images/configuring-the-ELK-server.png)
  
- Update line 3, the hosts line, in [filebeat-playbook.yml](https://github.com/nabouneama/Project-1-Elk-Stack/blob/main/Ansible/roles/filebeat-playbook.yml) and the [intall-elk.yml](https://github.com/nabouneama/Project-1-Elk-Stack/blob/main/Ansible/install2-elk.yml) to identify which vm each playbook will be downloaded on.
 
- Run the playbook, and navigate to http://52.225.73.227:5601/app/kibana to check that the installation worked as expected.

_Commands to download playbook and update files_
- cp ansible.cfg /etc/ansible
- nano hosts
    [webservers]
    10.0.0.5 ansible_python_interpreter=/usr/bin/python3
    10.0.0.6 ansible_python_interpreter=/usr/bin/python3
    
    [elk]
    10.1.0.4 ansible_python_interpreter=/usr/bin/python3
- exit hosts
- nano [filebeat-playbook.yml](https://github.com/nabouneama/Project-1-Elk-Stack/blob/main/Ansible/roles/filebeat-playbook.yml)
    -  go to line 3 and write (hosts: webservers)
- exit yaml file (ctrl + x) 
- mv filebeat-playbook.yml /etc/ansible/roles
- ls roles to make sure it moved 

- nano [intall-elk.yml](https://github.com/nabouneama/Project-1-Elk-Stack/blob/main/Ansible/install2-elk.yml)
    - go to line 3 and write (hosts: elk)
- exit yaml file (ctrl + x) 
- ansible-playbook filebeat-playbook.yml
- ansible-playbook install2-elk.yml
