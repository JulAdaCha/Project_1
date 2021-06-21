## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![image](https://user-images.githubusercontent.com/85324134/122702082-e564e500-d20b-11eb-8007-854a5468b95e.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible file may be used to install only certain pieces of it, such as Filebeat.

- /etc/ansible/filebeat-playbook.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available to customers, in addition to restricting DoS attacks to the network.
-If a server goes down, or needs to be updated, services will continue without interuption. The advantage of using a jump box only the jump box can access the virtual network via ssh. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- Filebeat monitors teh log files or locations specfied, collects log events and forwards them eiter to Elasticsearch or Logstash for indexing.
- Metricbeat is a metric shipper for monitoring a system and the processes running the system.

The configuration details of each machine may be found below.

| Name               | Function   | IP Address                                | Operating System |
|--------------------|------------|-------------------------------------------|------------------|
| JumpBoxProvisioner | Gateway    | Public: 137.135.25.164  Private: 10.0.0.4 | Linux            | 
| Web-1              | Server     | Public: N/A  Private:10.0.0.7             | Linux            |
| Web-2              | Server     | Public: N/A  Private:10.0.0.6             | Linux            |
| Web-3 (Redundancy) | Server     | Public: N/A  Private:10.0.0.5             | Linux            |
| Elk-1              | Monitoring | Public: 40.85.185.162  Private:10.1.0.4   | Linux            |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Kibana: Port 5061

Machines within the network can only be accessed by JumpBoxProvisioner.
- ELK-1 Public IP 40.85.185.162  Private IP 10.1.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses    |
|----------|---------------------|-------------------------|
| JumpBoxProvisioner | Yes       | 137.135.25.164 10.0.0.4 |
| Web-1              | No        | 10.0.0.7                |
| Web-2              | No        | 10.0.0.6                |
| Web-3              | No        | 10.0.0.5                |
| ELK-1              | Yes       | 40.85.185.162 10.1.0.4  |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it is fast, easy and prevents any overlooked vulneerabilities.
- Fast and easy set-up and added security.

The playbook implements the following tasks:
- Install docker.io
- Install python3-pip
- Download and start docker ansible container
- Download and start docker elk container
- Download images

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![image](https://user-images.githubusercontent.com/85324134/122702731-3b865800-d20d-11eb-8d7a-440708c6013e.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

| Name  | IP Address       |                
|-------|------------------|
| Web-1 | Private:10.0.0.7 |
| Web-2 | Private:10.0.0.6 |
| Web-3 | Private:10.0.0.5 |

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

| Name  | IP Address       |                
|-------|------------------|
| Web-1 | Private:10.0.0.7 |
| Web-2 | Private:10.0.0.6 |
| Web-3 | Private:10.0.0.5 |

These Beats allow us to collect the following information from each machine:
- Filebeat collects log data and shows them in the mointoring clusters.
- Metricbeat collects metrics and statistics and shows them in the output specified into Elasticsearch or Logstash. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook YAML file to an Ansible directory.
- Update the host file to include webservers and elk.
- Run the playbook, and navigate to Kibana to check that the installation worked as expected (http://[localhost]:5601/app/kibana).

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it? 
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?
- /etc/ansible/host
- 
- http://[localhost]:5601/app/kibana Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.
- ansible_playbook [filename.yml]
