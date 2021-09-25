# OSU-CS-Boot-Camp
Markis Allen Github  Reop
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

Update the path with the name of your diagram](Images/diagram_filename.png)
 1. https://github.com/allentech1905/OSU-CS-Boot-Camp/blob/master/Markis%20Allen%2C%20HW%2012%20Diagram.PNG

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _playbook_ file may be used to install only certain pieces of it, such as Filebeat.

  1.https://github.com/allentech1905/OSU-CS-Boot-Camp/blob/master/Ansible/WebServer%20Yml
  
  2.https://github.com/allentech1905/OSU-CS-Boot-Camp/blob/master/Ansible/Elk%20Installation
  
  3.https://github.com/allentech1905/OSU-CS-Boot-Camp/blob/master/Ansible/Filebeat%20Yml
  
  4.https://github.com/allentech1905/OSU-CS-Boot-Camp/blob/master/Ansible/Metricbeat%20Yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly avaiable, in addition to restricting access to the network.
What aspect of security do load balancers protect? What is the advantage of a jump box?
- Load Balancers acts as point of access for a service that is servicing multiple machines. 
- Jumpbox allows access to remote network, through SSH.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system resources.
What does Filebeat watch for? 
- System Log Files
What does Metricbeat record? 
- Records metrics and system resources usage in Elasticsearch

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| Web1`    | Webserver| 10.0.0.5   | Ubuntu           |
| Web2     | Webserver| 10.0.0.6   | Ubuntu           |
| Elk	     |ElasticSearch| 10.1.0.4| Ubuntu           |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 74.129.182.11

Machines within the network can only be accessed by Jumpbox.
Which machine did you allow to access your ELK VM? What was its IP address?
 1. Jumpbox
   - PublicIP: 104.42.218.227
   - PrivateIP: 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes/No              | 74.129.182.11
| Web 1 & 2| No                  |WebLB-13.88.41.138
| Elk Box  | Kibana -5601        |10.0.0.0/161

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
What is the main advantage of automating configuration with Ansible?
- Ansible allows for full automationof a specfic servierand reduces configuration errors.

The playbook implements the following tasks:
In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- Install Docker: Installs the core docker code to remote server
- Inatll Python3_pip: Allows installation os docker modules
- Install Docker Module: Tells the Pip Module to install the docker component modules
- Increase virtual memory: Increases memory for Elk Docker image
- Download and launch docker elk container: Downloads the elk  docker container and lanuches it.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
- https://github.com/allentech1905/OSU-CS-Boot-Camp/blob/master/Docker%20PS.PNG

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
List the IP addresses of the machines you are monitoring
1. 10.0.0.4
2. 10.0.0.5
3. 10.0.0.6
4. 10.1.0.4

We have installed the following Beats on these machines:
Specify which Beats you successfully installed
1. Filebeat
2. Metricbeat

These Beats allow us to collect the following information from each machine:
In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
 1. Filebeat collects system  type events such as logins.
 2. Metricbeat collects cpu usage and memory.


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the elk_install.yml file to /etc/ansible/roles/elk_install.yml.
- Update the hosts file to include... 10.1.0.4 ansible_python_interpreter=/usr/bin/python3
- Run the playbook, and navigate "http://10.1.0.4:5601/app/kibana" to check that the installation worked as expected.

Answer the following questions to fill in the blanks:
- Which file is the playbook? Where do you copy it? Elk_install.yml
- Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on? "Hosts", "10.1.0.4 ansible_python_interpreter=/usr/bin/python3"
- Which URL do you navigate to in order to check that the ELK server is running?"http://10.1.0.4:5601/app/kibana" 

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
1. ansible-playbook /etc/ansible/roles/elk_install.yml
2. ansible-playbook /etc/ansible/role/filebeat_playbook.yml

