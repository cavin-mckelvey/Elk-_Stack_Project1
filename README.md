## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![](Diagrams\azure_Redteam Network.drawio.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yaml file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.
 Placing VMS behind the load balancer allows the load to be spread out across multiple machines in case a machine goes down.

Advantage of a Jumpbox allows a single point of contact to the network from my personal IP address.   Also with ansible on the jumpbox multiple machines can be updated simultaniously

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system files.
Filebeat is used to monitor log data, events, and files, then forwards them to either Elasticsearch or Logstash.
Metricbeat is used to collect different metrics from the OS and services running on the server.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.6   |Linux Ubuntu 18.04|
| Web1     |webserver | 10.0.0.4   |Linux Ubuntu 18.04|
| Web2     |webserver | 10.0.0.5   |Linux Ubuntu 18.04|
| Elk      |monitoring| 10.1.0.4   |Linux Ubuntu 18.04|

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Personal IP Address

Machines within the network can only be accessed by Jumpbox VM via SSH.
-The Elk server can only be accessed_from the Jumpbox via SSH from Personal IP Address

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  | personal IP address  |
| Web1     | No                  | 10.0.0.4             |
| Web2     | No                  | 10.0.0.5             |
| ELK      | No                  | 10.0.0.6/personal IP |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
-The main advantage to ansible is having the ability to automate the installation process on many machines instead of each individual machine

The playbook implements the following tasks:
Installs Docker.io
Installs pip3 & the Python Docker Module
Allows and executes an increase in Virtual Memory
Downloads & launches the ELK container image, then opens the appropriate ports
Enables that ELK runs every time the machine is booted

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![](Diagrams\sudo_docker_ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
Web1 - 10.0.0.4
Web2 - 10.0.0.5


We have installed the following Beats on these machines:
Filebeat
Metricbeat

These Beats allow us to collect the following information from each machine:
Filebeat monitors log files and collect log events.
Metricbeat records metrics and statistical data from the operating system and from services running on the server

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the yml file to /etc/ansible/.
- Update the hosts file to include private IP addresses
- Run the playbook, and navigate to http://[your.VM.IP]:5601/app/kibana to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_/etc/ansible
You'll need to modify the private IP of the machines you'd like to configure in the /etc/ansible/ansible.cfg file.   How do I specify which machine to install the ELK server on versus which to install Filebeat on? update the /etc/ansible/hosts file.   
- _Which URL do you navigate to in order to check that the ELK server is running? http://[your.VM.IP]:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

For Filebeat:
curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat > /etc/ansible/filebeat-config.yml
filebeat-playbook:Filebeat Data

For Metricbeat:
curl https://gist.githubusercontent.com/slape/58541585cc1886d2e26cd8be557ce04c/raw/0ce2c7e744c54513616966affb5e9d96f5e12f73/metricbeat > /etc/ansible/metricbeat-config.yml
metricbeat-playbook:Metricbeat Data
