## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

- Ansible/diagram/NetworkDiagram.drawio.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the filebeat-playbook.yml, install-elk.yml, and metricbeat-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

  - Ansible/Pentest-DVWA.yml
  - Ansible/install-elk.yml
  - Ansible/filebeat-playbook.yml
  - Ansible/metricbeat-playbook.yml

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
- Load balancers protect your system from DDoS attacks by shifting the attacking traffic elsewhere. The advantage to having a jump box is that it gives access to the user from a single point that can be easily secured and monitored.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- Filebeat watches for any information in the file system that has been changed and when it happened.
- Metricbeat collects metrics and statistics and exports them to the output you desire.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.7   | Linux            |
| Web-1    | Server   | 10.0.0.5   | Linux            |
| Web-2    | Server   | 10.0.0.6   | Linux            |
| ELK-     | Server   | 10.3.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box virtual machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Home IP Address

Machines within the network can only be accessed by SSH.
- ELK Machine can only be accessed via SSH through 10.0.0.7

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  | Home IP Address      |
| Web-1    | No                  | 10.0.0.7             |
| Web-2    | No                  | 10.0.0.7             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The advantage of automating configuration is that you can input commands to multiple servers from a single playbook.

The playbook implements the following tasks:
- Install: docker.io
- Install: python-pip
- Install: docker
- Command: sysctl -w vm.max_map_count=262144
- Launch docker container for ELK: elk

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

- /Ansible/Screenshots/ELKProjectScreen_1.png


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.5
- Web-2 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat allows us to view and collect information on the changes done to the machine. Metricbeat then collects the metrics and the statistics. (Please see /Ansible/Screenshots/Kibana_Image.png)

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the .yml file to /etc/ansible/file/filebeat-config.yml.
- Update the /etc/ansible/host file to include the web servers and elk server IP addresses. 
- Run the playbook, and navigate to http://[publicip]:5601/app/kibana to check that the installation worked as expected.

**Bonus**
- Run command: ansible-playbook filebeat-playbook.yml
- This will complete the downloads and update the appropriate files for this project.