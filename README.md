# Mapr-install


                                      Ansible Playbook for installing Mapr Cluster


Prerequisite:

1.	Enable passwordless ssh form Ansible node to cluster nodes.
2.	Mapr user
3.	Flush iptables
4.	 

Installation:
 
1.	Enable EPEL repo and install ansible (yum install ansible )
2.	Copy ansible.zip and unzip it in / .
3.	add your patch file to /ansible/roles/mapr-patch/files/ dir  
4.	Update the host inventory file (/ansible/hostinv ) based on your requirement

Add the cluster node lists under the group [apps] and mention respective disk names.
Eg :

[apps]
10.163.172.147 disk1=/dev/sdb disk2= disk3=

If you are planning for 3 node cluster, update hostinv as below.

[apps]
10.163.173.111 disk1=/dev/sdc disk2=/dev/sdd disk3=
10.163.173.97 disk1=/dev/sda disk2=/dev/sdb disk3=/dev/sdc
10.163.173.50 disk1=/dev/sdc disk2=/dev/sdd disk3=/dev/sde

[cldb]
10.163.173.111

[apiservers]
10.163.173.97

[nfs]
10.163.173.50

Note : For 3 node cluster, ZK and cldb will be installed on all the three nodes. Add only one node under the group [cldb].  API server and NFS will be installed on respective nodes mentioned under the group.


4.	Run the playbook (install-maprcore.yml ) from the path /ansible as below
 
For single node/ multinode non secure cluster:
#ansible-playbook -e "cluster_name=test" -e "core=6.1.0" -e "mep=6.3.0"  install-maprcore.yml 

For multimode secure clusture.

#ansible-playbook -e "cluster_name=test" -e "core=6.1.0" -e "mep=6.3.0" -e "type=secure" install-maprcore.yml


