# Project-1
Contains information on first Azure Virtual Network deployment
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Images/Network-diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Playbook files may be used to install only certain pieces of it, such as Filebeat.

  - filebeat-playbook.yml
  - metricbeat-playbook.yml

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
- What aspect of security do load balancers protect? What is the advantage of a jump box? Load balancers protect the availablility aspect of CIA. A jump box provides a safe location that can only be ssh into and out of to other machines. It is hardened and works as another point of security in a virtual network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the VMs and VM system files.
- What does Filebeat watch for? Log files/events
- What does Metricbeat record? Metric data such as CPU usage, sudo failures, hosts, and inbound/outbound traffic.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](https://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.7   | Linux            |
| Web-1    | Webserver| 10.0.0.5   | Linux            |
| Web-2    | Webserver| 10.0.0.6   | Linux            |
| Web-3    | Webserver| 10.0.0.9   | Linux            |
| Elk-1    | Monitoring| 10.2.0.4  | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-box-provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
-47.12.68.191

Machines within the network can only be accessed by:
- Jump-box-provisioner (10.0.0.7)

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  | 47.12.68.191         |
| Web-1    | No                  | 10.0.0.7             |
| Web-2    | No                  | 10.0.0.7             |
| Web-3    | No                  | 10.0.0.7             |
| Elk-1    | No                  | 10.0.0.7             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- It takes far less time which leaves more time available to do other tasks

The playbook implements the following tasks:
- Install docker.io and pip3
- Install Docker python module
- Use more memory
- Download and launch a docker elk container
- Enable docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/docker_ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6
- 10.0.0.9

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
- Filebeat collects log data from target servesr and sends them to Elasticsearch. Filebeat consists of harvesters (which read the content of each single log file) and inputs (which finds the log files and starts a harvester for each one). For example, on the dashboard you would see syslogs by hostname, under that you could see "syslogd" under "process-name" which reads events over TCP and UDP.
- Metricbeat collects metric data such as operating system metrics, or data from services that are running on the target servers. One example of a system metric is CPU usage.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Update the Ansible hosts file to include the internal IPs of the target VMs. 
- Copy the playbook file to the Ansible control node.
- Update the config file to include your internal ELk Ip address
- Run the playbook, and navigate to http://<elk_external_IP>:5601/app/kibana or run curl http://<internal_IP_of_elk>:5601 to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it? filebeat-playbook.yml and metricbeat-playbook.yml. Copy into /etc/ansible/roles.
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on? Ansible hosts file. By specifying the name of the hosts from the hosts file (elk or webservers).
- _Which URL do you navigate to in order to check that the ELK server is running? http://<elk_external_IP>:5601/app/kibana
