Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![My Network Diagram](https://uci.bootcampcontent.com/Donaldk0775/donald-ko-my-homework/raw/master/Elk%20Stack%20Project/Images/My%20Network%20Diagram.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the .yml playbook file may be used to install only certain pieces of it, such as Filebeat.
We will need [filebeat-playbook.yml](https://uci.bootcampcontent.com/Donaldk0775/donald-ko-my-homework/blob/master/Elk%20Stack%20Project/Ansible-Playbooks/filebeat-playbook.yml) and [elk.yml](https://uci.bootcampcontent.com/Donaldk0775/donald-ko-my-homework/blob/master/Elk%20Stack%20Project/Ansible-Playbooks/elk.yml) to create the Elk-Server.


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly responsive, in addition to restricting access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system metrics.

The configuration details of each machine may be found below.

| Name                         | Function        | IP       | Operating System |
|------------------------------|-----------------|----------|------------------|
| Red-Team-Jump-Box-Provisoner | Gateway/Ansible | 10.0.0.4 | Linux (Ubuntu)   |
| DVWA-VM1                     | Docker-DVWA     | 10.0.1.4 | Linux (Ubuntu)   |
| ELK-Server                   | Database/ELK    | 10.0.1.5 | Linux (Ubuntu)   |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Red-Team-Jump-Box-Provisoner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
Personal IP Address

Machines within the network can only be accessed by SSH.

A summary of the access policies in place can be found in the table below.

| Name                         | Publicly Accessible | Allowed IP Addresses          |
|------------------------------|---------------------|-------------------------------|
| Red-Team-Jump-Box-Provisoner | No                  | Personal IP Address           |
| DVWA-VM1                     | No                  | 10.0.0.4                      |
| ELK-Server                   | No                  | 10.0.0.4  Personal IP Address |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. 
No configuration was performed manually, which is advantageous because automating configuration with Ansible allows us to only need to run playbooks with a single command that can configure multiple machines at once, instead of needing to perform it manually on each machine.


The playbook implements the following tasks:

*  Create a New VM (ELK-Server) with a private and public IP.
*  Download and configure the elk-docker container. Open the hosts.conf file with vi or nano and add a new group [elkservers] and the private IP of the ELK-Server machine to the group. Then create a new ansible playbook that will download, install, configure, and start the elk-docker container onto the ELK-Server machine.
*  Launch the Container and check if it is running successfully. SSH into the ELK-Server machine. Then run the command "sudo docker ps" to verify if the container is running.
*  Create New Inbound Security Rules that allow Ports: 5601 and 9200 from your personal network.
*  Open a browser window and type in the address bar [Public IP of ELK-Server:5601].

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
![Docker PS](https://uci.bootcampcontent.com/Donaldk0775/donald-ko-my-homework/raw/master/Elk%20Stack%20Project/Images/Docker_ps.jpg)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:

DVWA-VM1:10.0.1.4

We have installed the following Beats on these machines:

Filebeat:DVWA-VM1:10.0.1.4

Metricbeats:DVWA-VM1:10.0.1.4

These Beats allow us to collect the following information from each machine:

Filebeat allows us to collect log data on the machine it is installed on.

Metricbeats allows us to collect server and system metric data.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

*  Copy the [filebeat.yml](https://uci.bootcampcontent.com/Donaldk0775/donald-ko-my-homework/blob/master/Elk%20Stack%20Project/Ansible%20Configuration%20Files/filebeat.yml) and [metricbeat.yml](https://uci.bootcampcontent.com/Donaldk0775/donald-ko-my-homework/blob/master/Elk%20Stack%20Project/Ansible%20Configuration%20Files/metricbeat.yml) to the /etc/ansible/roles/files directory.
*  Update the configuration files with the private IP of the ELK-Server to the Kibana and Elasticsearch sections of the file.
*  Create a new ansible-playbook [filebeat-playbook.yml](https://uci.bootcampcontent.com/Donaldk0775/donald-ko-my-homework/blob/master/Elk%20Stack%20Project/Ansible-Playbooks/filebeat-playbook.yml) in the /etc/ansible/roles directory. This playbook will install, drop in the [filebeat.yml](https://uci.bootcampcontent.com/Donaldk0775/donald-ko-my-homework/blob/master/Elk%20Stack%20Project/Ansible%20Configuration%20Files/filebeat.yml) and [metricbeat.yml](https://uci.bootcampcontent.com/Donaldk0775/donald-ko-my-homework/blob/master/Elk%20Stack%20Project/Ansible%20Configuration%20Files/metricbeat.yml) from the /etc/ansible/roles/files directory, update the configuration files, and start the services for both.
*  Run the playbook and SSH back into the ELK-Server to check that the installation worked correctly.
*  Navigate to "PublicIPofELK-Server:5601" to check that the ELK server is running correctly.


The commands needed to run the Ansible configuration for the ELK Server are:


*  ssh RedAdmin@Red-Team-Jump-Box-Provisoner(PrivateIPofJumpbox)
*  sudo docker container list -a
*  sudo docker start "containername"
*  sudo docker attach "containername"
*  cd /etc/ansible
*  ansible-playbook elk.yml
*  cd /etc/ansible/roles
*  ansible-playbook filebeat-playbook.yml
*  Open up Kibana Web Portal (PublicIPofELKServer:5601)

Before running any of the ansible playbooks you must make sure to place all files in their correct directory.