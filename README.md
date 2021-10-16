## Executive Summary

This is a server network setup with Virtual Machines in AWS cloud. The 2 main servers are both accessed through a jumpbox running an ansible container. The job box can also communicate with an ELKbox container which has an ELK stack for monitoring file logs and metrics of the other webservers running DVWA. All 3 machines; the jumpbox and webservers 1 and 2 are in the webservers security group and accessible on port 22 SSH through the jump box, but are also accessible on HTTP through port 80 through a load balancer. The elk box is in an ELK security group which allows access to webservers 1 and 2. Webserver 2 is placed in an alternative subnet to ensure high availability zones are supported. 

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _Playbook.yml_ file may be used to install only certain pieces of it, such as Filebeat.


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly _available_, in addition to restricting _access_ to the network.
- 
Load Balancers protect the system from excessive traffic overload and a jump box allows access from a single secure access point to monitor the system. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the Data and system Logs. While Filebeat watches and collects data about file systems and exports it to Elasticsearch and Kibana. Meanwhile Metricbeat watches and collects metric data and exports it to a specified destination I.E. the ELK server

The configuration details of each machine may be found below.

Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name      | Function | IP Address   | Operating System |
|-----------|----------|--------------|------------------|
| Jump Box  | Gateway  | 172.31.7.186 | Linux            |
| ELK BOX   | ELK Stack| 172.31.7.97  | Ubuntu           |
| Webserver1| Webserver| 172.31.0.193 | Linux            |
| Webserver2| Webserver| 172.31.22.82 | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 18.191.237.107

Machines within the network can only be accessed by _JumpBox_.
- Jump Box 18.191.237.107:22

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses|
|----------|---------------------|---------------------|
| Jump Box | Yes                 |18.191.237.107       |
| ELK      | Yes(5601)           |172.31.7.186         | 
| Webserver| No(80)              |172.31.7.186         |
| Webserver| No(80)              |172.31.7.186         |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Limits the likelihood of manual errors and speeds the process

The playbook implements the following tasks:
- In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._ 

Install docker ansible on EC2 instance
copy the playbook and config file to the docker ansible container. 
Start the container
Attach the container
Start container bash shell
Edit hosts file
Edit config file
Run ansible playbook
Run ELK playbook
Run metricbeat
Run filebeat playbooks

- ...
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://drive.google.com/file/d/1kYfOnpYsvRAq76fzltvmozRwuhuXp_PH/view?usp=sharing

### Target Machines & Beats
This ELK server is configured to monitor the following machines, with installed beats:
- Webserver1 172.31.0.193 
  Webserver2 172.31.22.82 
  Metric Beat
  File Beat

These Beats allow us to collect the following information from each machine:
- File Beat collects log data from machines for later inspection. Metric Beat collects hardware statistics such as usage and network status

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook and config file to ELK.
- Update the Hosts file to include webservers allowable IP addresses.
- Run the playbook, and navigate to ELK to check that the installation worked as expected.

_Answer the following questions to fill in the blanks:_
- _ansible playbook copy to the /etc/ansible dir
  _Hosts file in /etc/ansible, update webservers group and create group for ELK server

- _Which URL do you navigate to in order to check that the ELK server is running? Kibana.com:5601
