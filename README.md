![Kubernetes Logo](https://raw.githubusercontent.com/kubernetes-incubator/kubespray/master/docs/img/kubernetes-logo.png)

KubeDeployer - Elite
======================
This Ansible Playbook deploys **Highly-Available(HA)** Kubernetes Cluster in **barebone VM's**. 

Maintainer
------
Leo li

Who may use this playbook:
--------------------------
This playbook can be used to automatically deploy a production-ready Kubernetes Cluster

Last verified Kubernetes version
--------------------------------
V1.11.3

Quick Start
------
#### Before start: 
1. Make sure [git](https://www.linode.com/docs/development/version-control/how-to-install-git-on-linux-mac-and-windows/) has been correctly installed on the environment;
2. Make sure [Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) has been correctly installed on the environment;
3. Make sure the user accout you are using can switch to root user on the target server;
4. You may need to check with IT admin see what subnet addresses (192.168.x.x/xx) can be used.
5. Enable root login over SSH by following [this instruction](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/v2v_guide/preparation_before_the_p2v_migration-enable_root_login_over_ssh).
6. Enable passwordless SSH access of all nodes by following [this instruction](https://www.tecmint.com/ssh-passwordless-login-using-ssh-keygen-in-5-easy-steps/).

### Deploy Highly-Available(HA) Kubernetes cluster:
1. Clone this Ansible Playbook on any server which has Ansible installed and can connect to the target VM's: 
```
git clone https://github.com/lilvyao/kubedeployer-ha.git
```
(You can also download the source code as zip from Git Hub)

2. Update ***kubedeployer-elite/inventory/host*** file by adding VM hostnames:
```
#Nodes

[masters]
<MASTER_NODE1>         ----> Add your master VM hostname. Only single master node is support by this playbook
<MASTER_NODE2>
...

[workers]
<WORKER_NODE1>        ----> Add your worker VM hostname(s). Note: Do not add the master node above here!!!
<WORKER_NODE2>
...

[all:vars]
ALL_IP={master1_ip},{master2_ip},...  ----> Add the ip addresses of all master nodes separated by ","
```
3. Review the default value of all of the role specific variables in each ***{role}/defaults/main.yml*** file.
4. If you need to customize the values of the role specific varialbles, please redefine the variables in ***{role}/vars/main.yml***.
5. Run the playbook:
```
ansible-playbook main.yml      # Please add "--connection=local" in the end if running from local
```

Verify you deployment
-------------

You can verify your Kubernetes cluster status by issuing the following command for verification:
```
kubectl get nodes
```

You can also follow [this](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#creating-a-deployment) 
tutorial to try deploying your first application to verify your Kubernetes environment.