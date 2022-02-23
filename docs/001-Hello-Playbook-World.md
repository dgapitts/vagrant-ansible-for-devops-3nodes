## Hello-Playbook-World - running on localhost


Following this example

```
[~/projects/vagrant-ansible-for-devops-3nodes] # cat helloworld.yml 
---
- name: This is a hello-world example
  hosts: localhost
  tasks:
    - name: Create a file called '/tmp/testfile.txt' with the content 'hello world'.
      copy:
        content: hello worldn
        dest: /tmp/testfile.txt
```

I was curious if the localhost might be within the context of the three inventory.ini files?

Unfortunately it appears it is not:
```
[~/projects/vagrant-ansible-for-devops-3nodes] #  ansible-playbook -i inventory.ini helloworld.yml 

PLAY [This is a hello-world example] *******************************************

TASK [Gathering Facts] *********************************************************
ok: [localhost]

TASK [Create a file called '/tmp/testfile.txt' with the content 'hello world'.] ***
changed: [localhost]

PLAY RECAP *********************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```

and here is what I have on my local laptop
```
[~/projects/vagrant-ansible-for-devops-3nodes] # cat /tmp/testfile.txt 
hello worldn
```     

