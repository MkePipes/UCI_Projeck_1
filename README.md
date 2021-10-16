## Executive Summary

This is a server network setup with Virtual Machines in AWS cloud. The 2 main servers are both accessed through a jumpbox running an ansible container. The job box can also communicate with an ELKbox container which has an ELK stack for monitoring file logs and metrics of the other webservers. All 3 machines; the jumpbox and webservers 1 and 2 are in the webservers security group and accessible on port 22 SSH through the jump box, but are also accessible on HTTP through port 80 through a load balancer. The elk box is in an ELK security group which allows access to webservers 1 and 2 via HTTP and SSH. Webserver 2 is placed in an alternative subnet to ensure high availability zones are supported. 

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _Playbook.yml_ file may be used to install only certain pieces of it, such as Filebeat.

- https://github.com/MkePipes/UCI_Projeck_1/blob/main/apacheplaybook.yaml
- https://github.com/MkePipes/UCI_Projeck_1/blob/main/Docker-file.yaml
- https://github.com/MkePipes/UCI_Projeck_1/blob/main/Ansible-config.yaml
- https://github.com/MkePipes/UCI_Projeck_1/blob/main/Elk%20playbook.yaml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology
![NEW_V2_Project_1_Diagram](https://user-images.githubusercontent.com/85429397/137603065-b67f83a6-9ef8-4a30-b29d-b5271d17126f.jpg)

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
 
Load Balancers protect the system from excessive traffic overload and a jump box allows access from a single secure access point to monitor the system. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the Data and system Logs. While Filebeat watches and collects data about file systems and exports it to Elasticsearch and Kibana. Meanwhile Metricbeat watches and collects metric data and exports it to a specified destination I.E. the ELK server

The configuration details of each machine may be found below.

| Name      | Function | IP Address   | Operating System |
|-----------|----------|--------------|------------------|
| Jump Box  | Gateway  | 172.31.7.186 | AWS-Linux        |
| ELK BOX   | ELK Stack| 172.31.7.97  | Ubuntu-Linux     |
| Webserver1| Webserver| 172.31.0.193 | AWS-Linux        |
| Webserver2| Webserver| 172.31.22.82 | AWS-Linux        |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Personal IP

Machines within the network can only be accessed by the JumpBox.
- Jump Box 172.31.7.186:22

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses|
|----------|---------------------|---------------------|
| Jump Box | Yes                 |Personal IP          |
| ELK      | Yes(5601)           |Any Public IP        | 
| Webserver| No(80)              |172.31.7.186         |
| Webserver| No(80)              |172.31.7.186         |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, this is advantageous because it limits the likelihood of manual errors 
and speeds the process

The playbook implements the following tasks:

Install docker ansible on EC2 instance
Start Apache
Run ansible install
Setup the Containers
Attach the container
Start container bash shell
Update hosts file
Update config file
Run ELK deployment
Run metricbeat install
Run filebeat install

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker_ps](https://user-images.githubusercontent.com/85429397/137578176-fbd6e673-c9c6-4e7b-b3e9-80711fa7e21f.PNG)

![V1docker_ps](https://user-images.githubusercontent.com/85429397/137578180-4403b21a-850f-426f-99f7-39379dda1770.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines, with installed beats:
- Webserver1 172.31.0.193 
  Webserver2 172.31.22.82 
  Metric Beat
  File Beat

The Beats which allow us to collect information from each machine are; FileBeat which collects log data from machines for later inspection and Metric which Beat collects hardware statistics such as usage and network status.

### Using the Playbook

SSH into the control node and follow the steps below:
- Copy the playbook and config file to ELK.
- Update the Hosts file to include webservers allowable IP addresses.
- Run the playbook, and navigate to ELK to check that the installation worked as expected.

- ansible playbook requires copy to the /etc/ansible dir
- Copy the Hosts file in /etc/ansible and update webservers group and create group for ELK server

- To verify that the ELK server is running navigate to Kibana.com:5601
