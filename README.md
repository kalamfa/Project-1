# Readme


## Automated ELK Stack Deployment



The files in this repository were used to configure the network depicted below.

Name of file: 
Project 1 - Network Diagram.png



These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - : Enter the playbook file._

  - Installing-elk.yml
  - filebeat-playbook.yml
  - metricbeat-playbook.yml



This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build



### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly ____avaiable____, in addition to restricting __ in-bound access___ to the network.


What aspect of security do load balancers protect? What is the advantage of a jump box?_

DDos attacks are prevented by diverting traffic through Load Balancers. 

The main feature of the Jumpbox includes single point of interfacing to the users to manage web servers at the backend. 



Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the ____file____ and system ____system metrics____.


What does Filebeat watch for?_ 

Filebeats collects and logs data on events basis and transfers it to Elastic search / logstash for the purpose of indexing.


[One of the facts that make Filebeat so efficient is the way it handles backpressure—so if Logstash is busy, Filebeat slows down it’s read rate and picks up the beat once the slowdown is over. Filebeat can be installed on almost any operating system, including as a Docker container, and also comes with internal modules for specific platforms such as Apache, MySQL, Docker, MariaDB, Percona, Kafka and more. There are default configurations and Kibana objects for these platforms. It ingests structured logs like audit logs, server logs, slow logs, and deprecation logs. 
Ref: https://logz.io/blog/beats-tutorial/
]


What does Metricbeat record?_ 

Metricbeats collects system configuration / information and services including OS platforms / versions and transfers it to Elastic search / logstash for the purpose of output. Information such as CPU to memory, Redis to NGINX, and etc. 


[ it monitors server and create an Elasticsearch index which are defined in Kibana
Ref: https://logz.io/learn/complete-guide-elk-stack/#installing-elk
]


The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.


| Name       | Function              | IP Address     | Operating System |
|------------|-----------------------|----------------|------------------|
| JUMP BOX   | GATEWAY               | 137.135.59.247 | LINUX            |
| WEB-1      | WEBSERVER             | 10.1.0.11      | LINUX            |
| WEB-2      | WEBSERVER             | 10.1.0.12      | LINUX            |
| ELK-SERVER | MONITORING/ELK Server | 10.2.0.4       | LINUX            |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the __ jump box provisioner ___ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:



Add whitelisted IP addresses_

99.232.83.*** (*** used for security reason)

Machines within the network can only be accessed by __ jump box provisioner___.



Which machine did you allow to access your ELK VM? What was its IP address?_


Machines within the network can only be accessed by the Jumpbox-Provsional

The IP address is	10.2.0.4


A summary of the access policies in place can be found in the table below.

| NAME       | PUBLICLY ACCESSIBLE  | ALLOWED IP ADDRESS                                            |
|------------|----------------------|---------------------------------------------------------------|
| JUMP BOX   | YES(from Local Host) | 99.232.83.*** / Local Host IP (*** used security reason)
| WEB-1      | NO                   | 10.2.0.4                                                      |
| WEB-2      | NO                   | 10.2.0.4                                                      |
| ELK-SERVER | NO                   | 10.2.0.4                                                      |




### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

What is the main advantage of automating configuration with Ansible? _

Following are the main advantages of the automating configurations with Ansible:
-Free Accessibility: Ansible is an open-source/free tool.
-Easy of Use: It is very simple to set up and use, no special coding skills are required to use playbooks of Ansible.
-Scalability: Ansible allows us to model even highly complex Technology environment and workflows. 
-Flexibility: Can orchestrate the entire application environment no matter where it’s deployed, can also customize it as per the requirements.
-Lesser Dependency: Being Agentless, doesn’t need to install any other software or firewall ports on the client systems that needs to be automated and doesn’t even required to set up a separate management structure.
-Efficiency: Since doesn’t need to require installations of any extra software, much room spared for for application resources on server.


The playbook implements the following tasks:



- Install-elk.yml: This playbook is used to configure the ELK server. It installs the downloads and installs docker, and the pulls correct container into ELK VM. It configures the machine to use more memory. And has a 
restart policy in place start elk container every time the machine boots. It configures that ports 5601 to be used to host the Kibana GUI.

- filebeat-playbook.yml: The playbook configures filebeat for the kibana GUI. This playbook downloads, installs and configures filebeat correctly. It starts the filebeat service, and has a restart policy in place for it to run
on systemboot

- metricbeat-playbook.ymk: The playbook configures metricbeat for the kibana GUI. This playbook downloads, installs and configures metricbeat correctly. It starts the metricbeat service, and has a restart policy in place for it to run
on systemboot





In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._

Install docker.io
Install pip3
Install Docker python module
Increase virtual memory
Download and launch a docker
- ...
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.



Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)


CONTAINER ID   IMAGE          COMMAND                  CREATED      STATUS      PORTS                                                                              NAMES
d169fe79fbd8  sebp/elk:761   "/usr/local/bin/star…"   4 days ago   Up 2 days   0.0.0.0:5044->5044/tcp, 0.0.0.0:5601->5601/tcp, 0.0.0.0:9200->9200/tcp, 9300/tcp   elk










### Target Machines & Beats

This ELK server is configured to monitor the following machines:

List the IP addresses of the machines you are monitoring_
-Private IPs of Web-1 and Web-2

This ELK server is configured to monitor the following machines:

NAME	IP ADDRESSES
WEB-1	10.1.0.11
WEB-2	10.1.0.12


We have installed the following Beats on these machines:

Specify which Beats you successfully installed_

Microbeats.


These Beats allow us to collect the following information from each machine:


In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. 
E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

Filebeat - collects data about the file system; collects log events specified by log files and location.

Metricbeat - collects machine metrics, such as uptime.and statistics from servers. 
The metrics could vary from system resources to metrics of services being run on the given system.






### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 


SSH into the control node and follow the steps below:
- Copy the ___ playbook __ file to ___ Ansible Control Node __ 
i.e. Copy the yaml file to /etc/ansible/roles

- Update the ___ hosts __ file to include webserver and elk
i.e. Update the hosts file to include private IP of ELK-Server

- Run the playbook, and navigate to ____ to check that the installation worked as expected.
i.e Run the playbook, and navigate to ELK-Serverto check that the installation worked as expected.


- _Which file is the playbook? Where do you copy it?_
- Install-elk is the playbook. It is copied into /etc/ansible/roles

- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- The host file is updated to make Ansible run the playbook on a specific machine. We specify the [elk] header followed by the IP of machine ensure ELK-stack is installed in the correct machine. We declaree the private IPs 
of Web-1 and Web-2 under [webservers] to ensure filebeat is installed on the correct machine. 

-_Which URL do you navigate to in order to check that the ELK server is running?
- We navigate following to access the kibana-GUI
http://http://52.142.13.43/:5601/app/kibana#/
