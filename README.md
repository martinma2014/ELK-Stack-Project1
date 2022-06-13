# ELK-Stack-Project1
Utilized Microsoft Azure to create a virtual network and configure four stacked servers. Set up a cloud monitoring system to oversee activity and loggings across those servers.

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

<img width="821" alt="Screen Shot 2022-06-13 at 9 34 48 AM" src="https://user-images.githubusercontent.com/94402616/173401879-67f68057-03b2-46ac-8ec2-31bb8125aa30.png">


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - https://github.com/martinma2014/ELK-Stack-Project1/blob/main/playbook%20files

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting unauthorized to the network.
- Load balancers protect the availability of the data by distributing the load across multiple servers. This can help protect against attacks affecting the availability of the servers and their data, such as Denial of Service (DoS) attacks. The advantage of a jump box is to limit access to servers that are not accessible from the internet, except thru the jump box.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the metrics and system system logs.
- Filebeat records system logs, such as logon attempts while Metricbeat records metric data, such as cpu usage.


The configuration details of each machine may be found below.

| Name     | Function             | IP Address              | Operating System                        |
|----------|----------------------|-------------------------|-----------------------------------------|
| Jump Box | Gateway              | 40.78.45.208 / 10.0.0.7 | Linux Ubuntu Server 18.04 LTS           |
| ELK      |ELK SERVER            | 10.1.0.4                | Linux Ubuntu Server 18.04 LTS           |
| web 1    |DVWA Server           | 10.0.0.5                | Linux Ubuntu Server 18.04 LTS           |
| web 2    |DVWA Redundancy Server| 10.0.0.6                | Linux Ubuntu Server 18.04 LTS           |
| web 3    |DVWA Redundancy Server| 10.0.0.9                | Linux Ubuntu Server 18.04 LTS           |
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the gateway machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 8.4.123.106



Machines within the network can only be accessed by the Jumpbox gateway machine at 10.0.0.4.


A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 |   8.4.123.106        |
| ELK      | Yes                 |   8.4.123.106        |
| web 1    | No                  |   10.0.0.7           |
| web 2    | No                  |   10.0.0.7           |
| web 3    | No                  |   10.0.0.7           |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it ensures consistency across the board, and that you would not have to worry about individual configurations being the same.

The playbook implements the following tasks:
- 1.Install docker
- 2.Install Python3-pip
- 3.Install the docker using pip3
- 4.Increase virtual memory
- 5.Download and launch the elk:761 docker web container and allowed the following published ports to be permitted access: 5601:5601 9200:9200 5044:5044
- 6.Enable the docker service

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

<img width="1016" alt="Screen Shot 2022-06-13 at 7 35 32 AM" src="https://user-images.githubusercontent.com/94402616/173402015-f1929d33-99bf-4eb8-bcf9-8cb0b9487e9c.png">


### Target Machines & Beats
This ELK server is configured to monitor the following machines:

| Name     | IP Address      |
|----------|-----------------|
|web 1     | 10.0.0.5        |
|web 2     | 10.0.0.6        |
|web 3     | 10.0.0.9        |

We have installed the following Beats on these machines:
- Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat forwards and centralizes log data from your target machines. It monitors the log files that you specify, ie. server logs such as login attempts. It collects the log events, then forwards the data to the ELK server.

- Metricbeat collects the machine metrics and statistical data, such as CPU usage, memory usage and inbound/outbound traffic and sends the data to the ELK server.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the configuration and playbook YAML file to /etc/ansible/files folder.
- Update the configuration file to include ELK server IP address 10.1.0.4
- Run the playbook, and navigate to Kibana to check that the installation worked as expected.

- _Which file is the playbook? Where do you copy it?_
  - filebeat-playbook.yml and metricbeat-playbook.yml; copied into /etc/ansible/files/
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
  
  -filebeat-config.yml, metricbeat-config.yml; Edit in beat configuration file templates

