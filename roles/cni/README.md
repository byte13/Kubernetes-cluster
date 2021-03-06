# Container network interface
This Ansible role installs Container Runtime Interfaces (CNI) in a Kubernetes cluster.   
Note that the playbook detects if target OS is Ubuntu or Rocky-Linux/Centos/Redhat and runs respective tasks.   
So there are variables specific to each OS.   

Fully tested using :
* Ansible 2.9.6 on Ubuntu 20.04 LTS
* Rocky-linux 8 as Kubernetes cluster nodes (should work on CentOS 8 and RedHat 8 as well)
* CRI-O 1.23 as container runtime

## Main steps to execute this Ansible playbook :
1. Possibly adjust variables in role/cni/var/main.yml.
2. Ensure that the following variables values don't confict/overlap with your enterprise IP addresses ranges
* k8s_pods_subnet
* k8s_pods_subnetmask

3. Choose one CNI provider, only, setting the folloing variable respectively to target OS :
* centos_cni
* ubuntu_cni  
  
Calico, only has been fully tested with this playbook, yet, but one could select Antrea, Cilium of Weave CNI instead.
## Directory structure :
```
.
├── defaults
│   └── main.yml
├── files
├── handlers
│   └── main.yml
├── meta
│   └── main.yml
├── README.md
├── tasks
│   ├── main.yml
│   ├── rocky-linux_master.yml
│   ├── rocky-linux_workers.yml
│   └── ubuntu_master.yml
├── templates
│   ├── calico_crd.j2
│   └── calico_IPPools.j2
├── tests
│   ├── inventory
│   └── test.yml
└── vars
    └── main.yml
```
# TODO
* Full tests with Antrea, Cilium and Weave CNI's
* Full tests with Kubernetes nodes running Ubuntu 20.04 LTS or higher

