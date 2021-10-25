# AnsibleVagrant

## Team 16

### Alan Xu, Logan Powell, Elle Summerfield

### Documentation

Because almost everything is automated in this assignment, there is not much explanation needed for code execution.

We simply call `vagrant up` or `vagrant provision` (if the VM is up and running already), which provisions the Vagrant machine (necessary installations, file copies, etc.), which in turn executes the master Ansible playbook. The master playbook then calls various child playbooks (included in `/tasks`), which perform tasks such as creating the Cloud VMs, installing the necessary packages, and starting the Zookeeper server and Kafka Brokers as necessary.  

## Demo

Below are screenshots of all of the completed tasks:

#### VM2 and VM3 Created
![Alt text](/Progress_Screenshots/VM3_Ansible_Creation.png?raw=true "VM2 and VM3 Created")

#### Install Necessary Packages
![Alt text](/Progress_Screenshots/Package_Installations.png?raw=true "Install Necessary Packages")

#### Kafka Installed on VM2 and VM3
![Alt text](/Progress_Screenshots/Kafka_Download_VM2_VM3.png?raw=true "Kafka Installed on VM2 and VM3")

#### Unzip Kafka
![Alt text](/Progress_Screenshots/Kafka_Unzip.png?raw=true "Unzip Kafka")

#### Zookeeper Started on VM2
![Alt text](/Progress_Screenshots/Zookeeper_Started_VM2.png?raw=true "Zookeeper Started on VM2")

#### Kafka Started on VM2
![Alt text](/Progress_Screenshots/Kafka_Started_VM2.png?raw=true "Kafka Started on VM2")

#### Kafka Started on VM3
![Alt text](/Progress_Screenshots/Kafka_Started_VM3.png?raw=true "Kafka Started on VM3")

#### CouchDB Installed on VM3
![Alt text](/Progress_Screenshots/CouchDB_Installed.png?raw=true "CouchDB Installed on VM3")

#### Topic Data Sent to DB via Consumer Code
![Alt text](/Progress_Screenshots/CouchDB_topic_data_sent_Consumer.png?raw=true "Topic Data Sent to DB via Consumer Code")
