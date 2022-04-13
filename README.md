## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)
(Diagrams/JRW-Project-Cloud-Security-and-Virtualization-Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to recreate the entire deployment pictured above. Alternatively, select portions of the .yml file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly accessible, in addition to restricting access to the network.
- Load balancers help protect the availability of resources. They protect the server/services from being overwhelmed with requests by distributing the load/requests to additional servers or microservices. It also protects the availability of the resource to those attempting to access it. In the case of a Denial of Service Attack, it can distribute those requests amongst resources to keep the service running and responsive. The advantage of using a jumpbox is it can act as a secure gateway to the rest of the VMs on your network and a single point of entry, limiting the attack surface of your services. Securing and monitoring this node is much easier than applying the same measures to each individual VM on your network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system logs.
- Filebeat monitors log files and locations we specify
- Metricbeat records metrics and can send them Elasticsearch
 

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.1.0.4   | Ubuntu 18.04     |
| Web-1    |Web Server| 10.1.0.5   | Ubuntu 18.04     |
| Web-2    |Web Server| 10.1.0.6   | Ubuntu 18.04     |
| ELK      |Monitoring| 10.0.0.4   | Ubuntu 18.04     |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- My Personal IP Address

Machines within the network can only be accessed by Jumpbox.
- The ELK VM can only be accessed by the Jump-Box-Provisioner machine (10.1.0.4)

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  | PersonalIP           |
| Web-1    | No                  | 10.1.0.4             |
| Web-2    | No                  | 10.1.0.4             |
| ELK      | No                  | 10.1.0.4 & PersonalIP|

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because
after you've successfully setup your configuration file the way you desire, you can easily use that file to create and update any number of additional configured machines and reduce the risk of future manual typing errors.

The playbook implements the following tasks:
- installs docker.io
- installs pip3 (python3)
- install docker python module
- increase virtual memory
- download and launch a docker elk container with published ports
- enable docker service on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.1.0.5
- Web-2 10.1.0.6

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeats collects log events from logfiles and forwards them to Elasticsearch for indexing
- Metricbeats sends the metrics and statistics it collects to Elasticsearch 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the .yml file to /etc/ansible/roles
- Update the hosts file to include the private ip addresses of the web servers and elk server
- Run the playbook, and navigate to http://<ELK.ExternalIP>:5601/app/kibana to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- Update hosts file under /etc/ansible to make Ansible run the playbook on a specific machine giving the IP address and specifying the version/location of python to use. You can label groups [webservers] and list the private IPs for the servers to run, and  [ELK] and list the IP and which version of python to run.
- Check ELK Server is running by visiting http://168.62.208.119:5601/app/kibana#/home?_g=0
