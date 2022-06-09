
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:
- The ELK Network comprises of 4 Virtual Machines, a load balancer and 2 security Groups all held within the Red_Team_Resource_Group. Two of the virtual machines (Web-1 and Web-2) feed metric data through to the ELK virtual machine which is then fed through to Kabana when running. 
- Access to all machines is limited to my personal device through the Security Group rules which is locked from other Public IP addresses. 
  - Mectricbeat and Filebeat have been configured on all machines with data flowing through the ELK machine
  - Web-1 and Web-2 are having their data monitored through the Beat programs. 
- An ansible machine has been built and can be reached through the Jump_Box_Provisioner Virtual Machine. After SSH'ing into the Jump-Box users can then access their Ansible container. 


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly secure, in addition to restricting access to the network.
- Load balances allow the system to spread the data across multiple machines to help counter DDoS attacks on any of the systems. The allows the system to be accessed by users more readily. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system metrics.
- Filebeat monitors and keeps track of log data within a system. You can flag specific data for the system to look for or simply keep track of all log data within a system. 
- Metricbeat monitors data into a server which could include time spent, data downloaded, visitor source information and keeps track of all of these statistics. 

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web-1    | Network         | 10.0.0.5   | Ubuntu           |
| Web-2    | Network         | 10.0.0.6   | Ubuntu           |
| ELK VM   | Data Collect.| 10.1.0.4   | Ubuntu           |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Local Public IP updated from VPN usage

Machines within the network can only be accessed by SSH.
- The Jump_Box_Provisioner was the only machine that had access to the ELK machine directly, the Jump Box's IP was 20.213.237.142

Web-1 and Web-2

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No              | 101.179.132.203   |
| Web-1         | No                    |      10.0.0.4                |
| Web-2         |   No                  |    10.0.0.4                  |
| ELK-Virtual-Machine       |   No                  |    10.0.0.4                  |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Ansible gives the person in charge of updating machines the option to update several machines in one script rather than updating each machine individually. 

The playbook implements the following tasks:
- Install the Docker function
- Start the Ansible docker
- Attach to the Ansible Docker
- Run functions required on machines form the Docker

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 20.213.252.252

We have installed the following Beats on these machines:
- _Metricbeat and Filebeat_

These Beats allow us to collect the following information from each machine:
- Filebeat monitors and keeps track of log data within a system. You can flag specific data for the system to look for or simply keep track of all log data within a system. Metricbeat monitors data into a server which could include time spent, data downloaded, visitor source information and keeps track of all of these statistics. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ansible file to the Jump-Box.
- Update the config file to include the IP addresses of the Virtual Machines in the network and created a ELK section for the last Virtual Machine.
- Run the playbook, and navigate to Kabana to check that the installation worked as expected.

- Which file is the playbook? Where do you copy it?
 - config_playbook.yml 
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?
- ansible.cfg
- Which URL do you navigate to in order to check that the ELK server is running?
- http://20.213.237.142:5601/app/kibana
