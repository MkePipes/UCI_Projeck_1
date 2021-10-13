## Executive Summary

This is a server network setup with Virtual Machines in AWS cloud. The 2 main servers are both controlled by a jumpbox running an ansible container. The job box can also communicate with an ELKbox container which has an ELK stack for monitoring file logs and metrics of the other 3 machines. The 3 machines of jumpbox and webservers 1 and 2 are in the web servers security group and only accessible on port 22 through the jump box or elk box, but are accessible to HTTP on port 80 through a load balancer. The elk box is in an ELK security group which allows access from host machine and to webservers 1 and 2. Webserver 2 is placed in an alternative subnet to ensure high availability zones are supported. 

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://drive.google.com/file/d/1OFcAZX2yN13-4UjMkYYxWX5zjvW3JdKb/view?usp=sharing

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _Playbook.yml_ file may be used to install only certain pieces of it, such as Filebeat.
 https://docs.google.com/document/d/1sTuOtZqOKwTT1FpQ6o4_y3mIJwqDKz2hQPcFpsRIu_0/edit?usp=sharing 

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

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _Data_ and system _Logs_.
- What does Filebeat watch for?_ Filebeat watches and collects data about file systems and exports it to Elasticsearch and Kibana
- What does Metricbeat record?_ Metricbeat watches and collects metric data and exports it to a specified destination

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name      | Function | IP Address   | Operating System |
|-----------|----------|--------------|------------------|
| Jump Box  | Gateway  | 18.223.158.79| Linux            |
| ELK BOX   | ELK Stack| 18.116.86.140| Ubuntu           |
| Webserver1| Webserver| 18.191.64.207| Linux            |
| Webserver2| Webserver|18.220.254.140| Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the _JumpBox_and ELK_ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 192.168.1.38

Machines within the network can only be accessed by _JumpBox_.
- Jump Box 18.223.158.79:22

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses|
|----------|---------------------|---------------------|
| Jump Box | Yes                 |18.223.158.79        |
| ELK      | Yes?                |18.116.86.140        | 
| Webserver| No                  |18.191.64.207        |
| Webserver| No                  |18.220.254.140       |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Limits the likelihood of manual errors and speeds the process

The playbook implements the following tasks:
- In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._ 

Install docker ansible on EC2 instance
copy the key.pem to the docker ansible container. 
Download the docker image
Copy key.pem into new container
Start the container
Attach the container
Start container bash shell
Edit hosts file
Edit config file
Run ansible playbook
Run ELK playbook

- ...
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://drive.google.com/file/d/1kYfOnpYsvRAq76fzltvmozRwuhuXp_PH/view?usp=sharing

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- JumpBox 18.223.158.79
  Webserver1 18.191.64.207
  Webserver2 18.220.254.140

We have installed the following Beats on these machines:
- Metric Beat
  File Beat

These Beats allow us to collect the following information from each machine:
- File Beat collects log data from machines for later inspection. Metric Beat collects hardware statistics such as usage and network status

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _Key.pem_ file to _ELK_.
- Update the _Hosts_ file to include...
- Run the playbook, and navigate to _ELK_ to check that the installation worked as expected.

_Answer the following questions to fill in the blanks:_
- _ansible playbook copy to the /etc/ansible dir
  _Hosts file in /etc/ansible, update webservers group and create group for ELK server

- _Which URL do you navigate to in order to check that the ELK server is running? Kibana.com:5601

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

https://docs.google.com/document/d/1uHj2aJyP09VavkrS2NzQ9VKB1x6UQ-2ok2Xv8VrMGMo/edit?usp=sharing

