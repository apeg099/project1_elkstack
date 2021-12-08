## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.
![image](https://user-images.githubusercontent.com/89222100/145265087-7f01f593-ea8b-4aca-94bd-746a7f047b08.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the my-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

- /etc/ansible/install-elk.yml

![image](https://user-images.githubusercontent.com/89222100/145271932-3f5322a0-a7fd-4e80-bfba-2bea76abda6d.png)

This document contains the following details:

- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly redundant and efficient, in addition to restricting inbound access to the network.

- Load balancer distributes traffic from clients to servers efficiently and effortlessy. Therefore, clients do not have to understand the topology or the mechanism of servers to decide where to access. It offers enhanced user experience with simple scaling of web servers, resillience, and additional layer of security.

What is the advantage of a jumpbox?
- Utillizing a jumpbox allows admin to audit for traffic with ease and manage user accounts by sitting in between a secure zone and untrusted zone.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the jumpbox and system networks.
- Filebeats watches over file changes on the machines
- Metricbeats gathers metrics from operating systems and services running on the servers.

The configuration details of each machine may be found below.

| Name     | Function  | IP Address               | Operating System |
|----------|-----------|--------------------------|------------------|
| Jump Box | Gateway   | 10.0.0.6 / 20.120.31.137 | Linux            |
| Web-1    | DVWA      | 10.0.0.7                 | Linux            |
| Web-2    | DVWA      | 10.0.0.8                 | Linux            |
| Web-3    | DVWA      | 10.0.0.9                 | Linux            |
| ELK-VM   | Monitor   | 10.1.0.4 / 20.83.126.21  | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- My home network public address | 45.50.0.199

Machines within the network can only be accessed by ssh connection through a jumpbox.
- Jumpbox VM is the only machine that has access to ELK VM with private IP address | 10.0.0.6.
- Web-VMs can be accessed via a jumpbox | 10.0.0.6.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| JumpBox  | No                  | 45.50.0.199          |
| Web-1    | No                  | 10.0.0.6             |
| Web-2    | No                  | 10.0.0.6             |
| Web-3    | No                  | 10.0.0.6             |
| ELK-VM   | No                  | 10.0.0.6             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Free of charge because ansible is an open-source tool.
- Simple set up.
- Ability to simplify complex workflow.
- High efficiency due to automated deployment and no extra software installment is needed, which in turns provide more space for other required resources.

The playbook implements the following tasks:
- Install docker.io
- Install pip3
- Install Docker python module
- Increase virtual memory
- Download and launch docker
- Automated configuration upon start

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![image](https://user-images.githubusercontent.com/89222100/145277297-128c087a-54e5-4cde-93e4-d3358904bf2b.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

| Name     | IP adresses |
|----------|-------------|
| Web-1    | 10.0.0.7    |
| Web-2    | 10.0.0.8    |
| Web-3    | 10.0.0.9    |

We have installed the following Beats on these machines:

- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:

- Filebeat collects log inforamtion about the file system, and also able to log specific files.
- Metricbeat collects metric information from the operating systems and services running on the servers.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

- Copy the install-elk.yml file to /etc/ansible.
- Update the /etc/ansible/hosts file to include ELK server (Web servers are pre-configured).
- Run the playbook, and navigate to http://[Elk-VM-ip:5601]/app/kibana to check that the installation worked as expected.
 
** To run the playbook, use the command:
  - ansible [playbook_name].yml

** To update the playbook, use the command:
  - nano [playbook_name].yml
