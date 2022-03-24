# Project-1-Elk-Stack
This include all the files and images that explain and show what happened in the process of doing the project.

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Diagrams/networking.png](https://github.com/nabouneama/Project-1-Elk-Stack/blob/main/Diagrams/networking.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

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

Load balancing ensures that the application will be highly _____, in addition to restricting _____ to the network.
- Load balancers distributes and divide the network traffic onto many servers which help increase the capacity of the users. They protect and ensures the availability of the information if one server went down or crashed. 
- A jumpbox is a system on a network that is used to access all the information needed within a more secured machine. It is used to protect the information and limit the people who have access to the information.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
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

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  | local host IP        |
| Web 1    | No                  | 10.0.0.4             |
| Web 2    | No                  | 10.0.0.4             |
| ELk vm   | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Ansible is easy to use and doesn't require coding skills. 
- It also helps with the representation of IAC Infrastructure as Code.
- It makes writing complex playbooks easy and able to be reused.

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Docker_ps_output](https://github.com/nabouneama/Project-1-Elk-Stack/blob/main/Images/verifying-the-container.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
