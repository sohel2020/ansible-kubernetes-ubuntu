# ansible-kubernetes-ubuntu task
This project aim is to create ansible playbook to provision into ubuntu bare metal server 

### Prerequisite
1. ansible 
2. git

###Setup Cluster steps:
**step-1:** Install ansible and git in your local ubuntu machine:-
```bash
$ sudo apt-add-repository -y ppa:ansible/ansible
$ sudo apt-get update
$ sudo apt-get install -y ansible git
```

**step-2:** Run ssh agent
```bash
$ eval $(ssh-agent -s)
```
**step-3:**  Add your ssh key (which you are using to login into the cluster)
```bash
$ ssh-add devops-key.pem
```
**step-4:** Navigate to your project directory
**step-5:** Add  your node IP address inside **hosts** file. Just below the [kubernete-minions] section.
**step-6:** Run playbook 
```bash
$ ansible-playbook -i hosts playbook.yml
```

This command will download kubernetes repository and build all kubernetes binarys for ubuntu. Then scp to the server node and run all kubernetes master and node components and also install kube DNS and UI addon. 

If your server is configured correctly then open your browser and hit:

http://54.152.145.109:8080/ui



## How can I deploy multi node cluster? 

Assume we're going to launch 1 master  and 2 nodes kubernetes cluster. In that case we need to change our `config-default.sh.j2` file.

<img style="float: right;" src="https://s15.postimg.org/leb8lfmnf/Selection_004.png"  />

You'll find `config-default.sh.j2` file under `roles/kubernete-deployer/templates/` and make change according to above images, where **a** indicate master and **i** indicate node/minion. As we're going to use 2 node so we need to change **NUM_NODES**. 

Now it's time to change inventory/hosts file. Insert your IP addresses. First IP will be master  and other 2 will be node. Please follow as you're seeing below images

<img style="float: right;" src="https://s11.postimg.org/436bdj3j7/Selection_007.png"  />

