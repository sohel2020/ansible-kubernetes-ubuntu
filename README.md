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