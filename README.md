## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![This is an image](https://github.com/EricF1525/UCI-Project1/blob/main/Images/Network%20Diagram.png)


These files have been tested and used to generate a live ELK deployment on AWS. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the filebeat-playbook.yaml file may be used to install only certain pieces of it, such as Filebeat.

- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


## Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Jump Box server is implemented to help streamline workflow from a central server. This allows the servers to be readily available to SysAdmins.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network. Working in layer 4, load balancers will help distribute traffic across servers helping reduce compute strain. This allows for increased user traffic and for high capacity deployments. In terms of Security, you're well taken care of as a Load Balancer can mitigate against DDoS attacks using the Off-Loading function. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to event logs and system applications.
Filebeat collects and forwards log events to both Elasticsearch and Logstash for further indexing. 
Metricbeat, when set, can periodically collect system metrics and send those to both Elasticsearch and Logstash. 

The configuration details of each machine are found below.

| Name        | Function | IP Address    | Operating System |
|-------------|----------|---------------|------------------|
| Jump Box    | Gateway  | 172.31.17.208 | Linux- AMI       |
| Webserver1  | Server   | 172.31.4.51   | Linux- AMI       |
| Webserver2  | Server   | 172.31.9.87   | Linux- AMI       |
| ELK         | Server   | 172.31.35.91  |     Ubuntu       |

## Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box server can be access via SSH on the internet. Only Local IP is allowed to establish such connection.

Machines within the network can only be accessed by Jump Box ( 172.31.17.208 )

Access policies can be found in the table below.

| Name        | Publicly Accessible |   Allowed IP Addresses   |
|-------------|---------------------|--------------------------|
| Jump Box    |  No                 |        Local IP          |
| Webserver1  |  Yes                |        0.0.0.0/0         |
| Webserver2  |  Yes                |        0.0.0.0/0         |
| ELK         |  No                 | Local IP & 172.31.17.208 |


## Elk Configuration

Ansible was used to automate configuration of the ELK machine. For starters, Ansible allows for application-deployment and is created using Ifrastructure as code. ELK stack was not configured manually so setup was relitively easy. 

The playbook implements the following tasks:
- Install Docker
- Increase vMemory 
- Install pip 
- Install docker python3
- Launch Docker contianer 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

<img width="1226" alt="Docker-ps-output" src="https://github.com/EricF1525/UCI-Project1/blob/main/Images/Docker%20ps.PNG">


## Target Machines & Beats
ELK stack monitoring:
- Webserver 1: IP 172.31.4.51
- Webserver 2: IP 172.31.9.87

The following Beats were installed: 
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat will collect log files and log events, and send them to Elasticsearch and Logstash. An example of what is expected, 
- Metricbeat collects metrics from the operating system and services on the server. 


## Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the Jump Box ( control node ) and follow the steps below:
- Move ansible playbook into ansible directory.
- Add ELK server IP address in the config file.
- Run the playbook, then navigate to Kibana via 5601 using ELK server IP address. 
