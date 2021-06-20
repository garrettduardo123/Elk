## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![ElkStack](https://user-images.githubusercontent.com/28407138/122657910-5d53e200-d11c-11eb-8445-6173466ce092.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the .yml file may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly efficient, in addition to restricting access to the network.


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the files and system performance.

The configuration details of each machine may be found below.


| Name     | Function                   | Ip Addr  | OS    |
|----------|----------------------------|----------|-------|
| Jump Box | Gateway                    | 10.0.0.1 | Linux |
| Web1     | DVWA Container             | 10.0.0.7 | Linux |
| Web2     | DVWA Container             | 10.0.0.8 | Linux |
| Elk VM   | Kibana + host of elk stack | 10.1.0.5 | Linux |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 10.0.2.15

Machines within the network can only be accessed by Jump Box.


A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box |     Yes             |Personal Device IP    |
| Elk Box  |     No              |        N/A           |
| Web1     |     No              |        N/A           |
| Web2     |     No              |        N/A           |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because this automation is leaps and bounds faster and allows for instant vms to be setup with the necessary modules.

The playbook implements the following tasks:
- You start with making sure that theres enough memory getting allocated, then you install docker and python3
- Next you download the sebp/elk:761 image and make sure ports that you need are open
- Also you must install a module that makes sure docker is restarted called systemd

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![dockerps](https://user-images.githubusercontent.com/28407138/122655667-f547d080-d108-11eb-9caf-81d1785e7f64.PNG)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.7
- 10.0.0.8

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat is a very powerful monitoring beat that is used to track file information and logs files coming in and out of systems and checking to see if they are malicious or       not, you get a ton of info like: ip, domain name, location(coords), and even websites being visited.
- Metricbeat is also a powerful tool that tracks system information and monitors system performance such as CPU usage and memory usage. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat/metricbeat install file to /etc/ansible.
- Update the /etc/ansible/hosts file to include ips of the vms that has the elk stack installed on it.
- Run the playbook, and navigate to http://(ELKVM_IP):5601 to check that the installation worked as expected.
 

# Commands needed to install and edit playbooks as needed

### Download and edit the `hosts` file in the /ansible directory
```
curl -L -O https://github.com/garrettduardo123/Elk/blob/main/Ansible/YML/hosts.txt

nano /etc/ansible/hosts
```
 Add your docker container IPs and Python3 under the webservers group
```
[webservers]

000.000.000.000 ansible_python_interpreter=/usr/bin/python3
000.000.000.000 ansible_python_interpreter=/usr/bin/python3
```
### Download the docker playbook:
```
curl -L -O https://github.com/garrettduardo123/Elk/blob/main/Ansible/YML/docker.yml
```

 Next edit the playbook 

   `nano docker.yml`

 At line 3 add `webservers` to the hosts file:
   ```
   hosts: webservers
   ``` 
### Download the filebeat playbook 
```
curl -L -O https://github.com/garrettduardo123/Elk/blob/main/Ansible/YML/filebeat.yml
```
 
  Download and if needed edit the filebeat config file
   
    curl -L -O https://github.com/garrettduardo123/Elk/blob/main/Ansible/YML/filebeat-config.yml
    
### Download the metricbeat playbook
```
curl -L -O https://github.com/garrettduardo123/Elk/blob/main/Ansible/YML/metricbeat.yml
```
 
   Download and if needed edit the metricbeat config file
 
    
    curl -L -O https://github.com/garrettduardo123/Elk/blob/main/Ansible/YML/metricbeat-config.yml
    
    
### Download the Elk Install playbook
```
curl -L -O https://github.com/garrettduardo123/Elk/blob/main/Ansible/YML/ElkInstall.yml
```
