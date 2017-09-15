=======
# Objectpools BETA

## Final release name is likely to be ObjectTiering

Put all stuff in here that helps to test, deploy, automate and run the ObjectTiering feature.

Repository is maintained by fabian@mapr.com and can be updated by everyone.

## Creating a set of EC2 nodes for your MapR cluster and one more node, to represent a client 

For the Beta-2 testing, there is no MapR-Installer support. You have to manually provision your 
set of nodes.

The first step of course, is to be able to create a set of nodes on AWS, to represent your MapR Cluster
and at least one client node. To do that, we are going to use Ansible and its 'ec2' module.

#### Install Ansible

Go to ansible.com and follow the instructions to install it for your desktop/laptop.

#### Using Ansible Playbooks

Playbooks are the input to Ansible. It uses a special YAML format. Playbooks contain plays and plays 
contain tasks. Each task uses a pre-defined Ansible-module (like yum/apt/file) to do a well defined
task. 

All the documentation is on ansible.com.

##### Launch your set of nodes.

*Playbook file*: launch_ec2_nodes.yml

This Playbook file uses the 'ec2' Ansible-module to launch the specified set of nodes. 

Here are steps that you need to do, before you can start running this playbook:
Step 1:
* Open the playbook file: launch_ec2_nodes.yml 
* Change the values of the variables specified in the *var* section, like  *region*, *instance_type* etc.
* There are additional variables, parameters like COUNT, NAME, that you will be overriding on the cmd line.
* Run the playbook like this:

$ ansible-playbook -i ./hosts ./launch_ec2_nodes.yml --extra-vars "COUNT=5 NAME=rajesh-citi-objpool2"

In the above command, note the following:
'hosts' : Ansible inventory file (required)
'launch_ec2_nodes.yml': Playbook 
 COUNT : Param in the Playbook. Specify the number of EC2 nodes required for the MapR Cluster
 NAME  : Param in the Playbook. Tag for your resources. 


