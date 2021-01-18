ummary

Following "Ansible 101 by Jeff Geerling" and pleased to have a 3 node cluser running with vagrant and ansible provisioning.

Had to tweak my inventory file 

    # Cannot handle SSH host authenticity prompts for multiple hosts
    # https://stackoverflow.com/questions/23074412/how-to-set-host-key-checking-false-in-ansible-inventory-file 
    ansible_ssh_common_args='-o StrictHostKeyChecking=no'


## First run


    ~/projects/vagrant-ansible-for-devops-3nodes$ ansible -i inventory.ini multi -a "hostname"
    192.168.60.4 | CHANGED | rc=0 >>
    orc-app1.dev
    192.168.60.6 | CHANGED | rc=0 >>
    orc-db.dev
    192.168.60.5 | CHANGED | rc=0 >>
    orc-app2.dev
