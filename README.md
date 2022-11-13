# Vagrant-Ansible-Kubernetes(VAK)

## Prerequisite/Setup
1. Enable Virtualization in your system
2. Install type-2 hypervisor such as [Oracle VirtualBox](https://www.virtualbox.org/wiki/Downloads)
3. Install [Vigrant](https://developer.hashicorp.com/vagrant/downloads)
4. Clone this repository

## Getting Started
- For detailed Kubernetes setup click [here](https://sunnykkc13.medium.com/kubernetes-setup-489ecb64a896) 
- Open the command line terminal then run
```
vagrant up
```
- it will start creating the virual machines.
- in vagrantfile, there are two servers mentioned i) masternode ii) workernode.
- Numbers of workernode can be added in servers array in the vagrantfile.
- Make sure the variables are same. The **role** variable is quite important.
- the cluster will be created as soon as ansible is completed on all machines.
> Note: Cilium is a CNI used in this case but it is still not installed.

- as soon as setup gets completed
- open two new terminal where the current directory should be the same
```
# in k8s-vagrant-ansible directory 
vagrant up masternode

#in another terminal
vagrant up workernode
```
- on masternode run `cilium install`. Wait till its completion
- as soon as it gets completed, the cluster is good to go.

```
# on masternode
kubectl cluster-info
kubectl get pods --all-namespaces
```