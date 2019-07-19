# Galera Test Environment (Including MaxScale)
###  3 Galera Nodes, 1 MaxScale Node

#### About

This automation project will use **Vagrant** to create 4 nodes in **Virtualbox**. The included **Ansible** playbook will work with both Ubuntu and CentOS systems.  You can choose to build a MariaDB Cluster or a Percona XtraDB Cluster. If you do not wish to build a virtual environment, you may alter the "inventory" file to include your own existing infrastructure and skip the **Vagrant** steps in the **Setup** section below.

#### Prerequisites

* [Git](https://git-scm.com/download/)
* [Vagrant](https://www.vagrantup.com/downloads.html)
* [Virtualbox](https://www.virtualbox.org/wiki/Downloads)
* [Ansible](http://docs.ansible.com/ansible/latest/intro_installation.html)

#### Setup

* `git clone https://github.com/toddstoffel/galera_demo.git`
* `cd galera_demo` 
* `vagrant plugin install vagrant-vbguest`
* `vagrant up`
* `ansible-playbook provision.yml` :arrow_left: **for MariaDB Cluster**
* `ansible-playbook provision.yml --extra-vars "provider=percona"` :arrow_left: **for Percona XtraDB Cluster**

#### Galera Node Access

* `vagrant ssh node1` :arrow_left: **Database Node 1**
* `vagrant ssh node2` :arrow_left: **Database Node 2**
* `vagrant ssh node3` :arrow_left: **Database Node 3**

#### MaxScale Node Access

* `vagrant ssh node4` :arrow_left: **MaxScale 1**

####  Clean Up

* `vagrant destroy --force`

#### Additional Notes:

While not important for this demonstration, please open the following ports between nodes when moving this project to real servers:

* **3306** For MySQL/MariaDB client connections and State Snapshot Transfer that use the mysqldump method.
* **4567** For Galera cluster replication traffic, multicast replication uses both **UDP** transport and **TCP** on this port.
* **4568** For Incremental State Transfer.
* **4444** For State Snapshot Transfer.
