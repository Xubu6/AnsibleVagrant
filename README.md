# AnsibleVagrant

## Team 16

### Alan Xu, Logan Powell, Elle Summerfield

### Documentation

Because almost everything is automated in this assignment, there is not much explanation needed for code execution.

We simply call `vagrant up` or `vagrant provision` (if the VM is up and running already), which provisions the Vagrant machine (necessary installations, file copies, etc.), which in turn executes the master Ansible playbook. The master playbook then calls various child playbooks (included in `/tasks`), which perform tasks such as creating the Cloud VMs, installing the necessary packages, and starting the Zookeeper server and Kafka Brokers as necessary.  
