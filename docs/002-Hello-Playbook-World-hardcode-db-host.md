## Hello-Playbook-World with hardcode `db` host

```
[~/projects/vagrant-ansible-for-devops-3nodes] # cat helloworld.yml 
---
- name: This is a hello-world example
  hosts: db
  tasks:
    - name: Create a file called '/tmp/testfile.txt' with the content 'hello world'.
      copy:
        content: hello worldn
        dest: /tmp/testfile.txt
```



```
[~/projects/vagrant-ansible-for-devops-3nodes] # cat inventory.ini 
# Application servers
[app]
192.168.60.4
192.168.60.5

# Database server
[db]
192.168.60.6

# Group 'multi' with all servers
[multi:children]
app
db

# Variables that will be applied to all servers
[multi:vars]
ansible_ssh_user=vagrant
ansible_ssh_private_key_file=~/.vagrant.d/insecure_private_key
# https://stackoverflow.com/questions/23074412/how-to-set-host-key-checking-false-in-ansible-inventory-file 
ansible_ssh_common_args='-o StrictHostKeyChecking=no'
```



```
[~/projects/vagrant-ansible-for-devops-3nodes] #  ansible-playbook -i inventory.ini helloworld.yml 

PLAY [This is a hello-world example] *******************************************

TASK [Gathering Facts] *********************************************************
ok: [192.168.60.6]

TASK [Create a file called '/tmp/testfile.txt' with the content 'hello world'.] ***
changed: [192.168.60.6]

PLAY RECAP *********************************************************************
192.168.60.6               : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```


```
[~/projects/vagrant-ansible-for-devops-3nodes] # vagrant ssh db
Last login: Tue Feb 22 21:22:11 2022 from 192.168.60.1
[vagrant@orc-db ~]$ uptime
 21:22:41 up  4:59,  1 user,  load average: 0,00, 0,01, 0,04
[vagrant@orc-db ~]$ ls -l /tmp/testfile.txt 
-rw-rw-r--. 1 vagrant vagrant 12 22 feb 21:22 /tmp/testfile.txt
[vagrant@orc-db ~]$ cat /tmp/testfile.txt
hello worldn[vagrant@orc-db ~]$ 
[vagrant@orc-db ~]$ 
```

