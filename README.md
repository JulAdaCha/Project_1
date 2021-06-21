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
- Filebeat monitors the log file data then combines the data into monitored clusters. Once a cluster is created it is shipped to Elasticsearch for indexing and analysis. Kibana is used to ensure the log files are being monitored and indexed and to visualize the analyzed data. 
- Metricbeat monitors metrics and statistics data. Once collected this data is shipped to Elasticsearch or Logstash for indexing and analysis. Kibana is used to ensure the metrics are being indexed and visualizes the analyzed data. 

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
- Local host IP Address and port 80 (HTTP). Public IP Address 137.135.25.164

Machines within the network can only be accessed by the ansible container through docker located on the Jup Box.
- The ELK-1 server is accessed by the ansible container inside theJumpBoxProvisioner using port 22 (SSH)
- The Kibana website is accessed using the ELK-1 public IP Address 40.85.185.162 using port 80 (HTTP)

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses    |
|----------|---------------------|-------------------------|
| JumpBoxProvisioner | Yes       | 137.135.25.164 10.0.0.4 |
| Web-1              | No        | 10.0.0.7                |
| Web-2              | No        | 10.0.0.6                |
| Web-3              | No        | 10.0.0.5                |
| ELK-1              | Yes       | 40.85.185.162 10.1.0.4  |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it is fast, easy and prevents any overlooked vulnerabilities.
- Fast and easy set-up
- Automation of daily tasks
- Additional security

The playbook implements the following tasks:
- Install docker.io
- Install python3-pip
- Download and start docker ansible container
- Download and start docker elk container
- Download images
- Open ports 5601:5601, 9200:9200 and 5044:5044
- Increase RAM by using vm.max_count 262144

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

| Name  | IP Address       |                
|-------|------------------|
| Web-1 | Private:10.0.0.7 |
| Web-2 | Private:10.0.0.6 |
| Web-3 | Private:10.0.0.5 |

- Metricbeat

| Name  | IP Address       |                
|-------|------------------|
| Web-1 | Private:10.0.0.7 |
| Web-2 | Private:10.0.0.6 |
| Web-3 | Private:10.0.0.5 |

These Beats allow us to collect the following information from each machine:
- Filebeat collects log files moves them into monitored clusters then ships the monitored clusters to Elasticsearch. Kibana verifies that Elasticsearch is running correctly and then provides visualization of the monitored data. 
- Metricbeat collects metrics and statistics from the systems and services running on a server such as Apache. Once data is collected it is shipped to either Elasticsearch or Logstash. Kibana provides visualization of the monitored servers.  

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy /ect/ansible/[current .deb file] to /etc/ansible/roles
- Update /etc/ansible/hosts and include webservers and elk as well as VM's Web-1, Web-1 and Web-3 with their private IP Addresses
- Run the playbook, then open Kibana to ensure the connection was installed. To access Kibana type url http://[localhost]:5601/app/kibana (http://40.85.185.162:5601/app/kibana)

Answer the following questions to fill in the blanks:
- Which file is the playbook? Where do you copy it? 
     /etc/ansible/install-elk.yml
- Which file do you update to make Ansible run the playbook on a specific machine?
     /etc/ansible/hosts
- How do I specify which machine to install the ELK server on versus which to install Filebeat on?
     /etc/ansible/filebeat-config.yml
- Which URL do you navigate to in order to check that the ELK server is running?
     http://[localhost]:5601/app/kibana

As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.
- ansible_playbook [filename.yml] (ansible playbook /etc/ansible/filebeat-playbook.yml)
