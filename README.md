## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

 ![Red Team Network Map jpg](https://user-images.githubusercontent.com/84424261/128754541-dd920dbc-5db3-4679-91da-e3dcdafa0889.jpg)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

  - install-elk.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.
- Load balancers distribute traffic to multiple servers at times of high volume to a website. This has the added advantage of protecting against DoS attacks and ensures that the network remains highly available. A jump-box, or provisioner, allows admins to securely accesss, monitor, configure a VM or network in the desired way. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system resources.
- Filebeat collects and forwards log data (files, events, etc.) to Elasticsearch or Logstash, which can later be analyzed using Kibana.
- Metricbeat will monitor and collect metrics and statistics from services running on a server and forwards them to either Elasticsearch or Logstash.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function   | IP Address | Operating System |
|----------|------------|------------|------------------|
| Jump Box | Gateway    | 10.0.0.4   | Linux            |
| Web 1    | Web Server | 10.0.0.5   | Linux            |
| Web 2    | Web Server | 10.0.0.6   | Linux            |
| Web 3    | Web Server | 10.0.0.8   | Linux            |
| Elk VM   | ELK        | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box virtual machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 73.86.196.21

Machines within the network can only be accessed by The Jump Box Provisioner.
- 52.146.0.126

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 73.86.196.21         |
| Web 1    | No                  | -                    |
| Web 2    | No                  | -                    |
| Web 3    | No                  | -                    |
| Elk VM   | Yes                 | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it allows for the streamlining of installations, updates, configurations, etc., to a server, as well as the automation of daily tasks.

The playbook implements the following tasks:

- This play will install docker and python3-pip.
- Install Docker module.
- It will increase and use more memory.
- Download and launch a Docker ELK container.
- And, finally, enable Docker automatically upon booting the machine.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Images/docker ps 1.png]

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6
- 10.0.0.8

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat will collect and forward log files and data, such as times and dates of events, to Elasticsearch or Logstash. Metricbeat will do the same for metrics and stats, such as CPU memory. Such data can later be compiled and analyzed using Kibana.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the configuration file from your ansible container to your Web VMs.
- Update the /etc/ansible/hosts file to include the IP address of the ELK and VM webservers.
- Run the playbook, and navigate to http://[your_elk_server_ip]:5601/app/kibana to check that the installation worked as expected.


- The playbookk file is /etc/ansible/filebeat-config.yml and it is copied to /etc/filebeat/filebeat.yml
- To make ansible run on a specific machine, update the filebeat-config.yml file. Use the hosts file to update the IP addressess and choose which to run on ansible.
- Navigate to Kibana/logs/DEB *tab*/, scroll down, and check that the beat is running.

Use the following useful commands to run filebeat:
- curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.6.1-darwin-x86_64.tar.gz
- tar xzvf filebeat-7.6.1-darwin-x86_64.tar.gz
- cd filebeat-7.6.1-darwin-x86_64/

*repeat the process for metricbeat*
