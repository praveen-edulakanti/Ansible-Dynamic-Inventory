# Ansible-Dynamic-Inventory
Download these ec2.ini and ec2.py files to the your project folder:
wget https://raw.githubusercontent.com/ansible/ansible/devel/contrib/inventory/ec2.py    
wget https://raw.githubusercontent.com/ansible/ansible/devel/contrib/inventory/ec2.ini

To test if everything is good, try executing the ec2.py by listing your resources:
./ec2.py --list


/etc/ansible/ansible.cfg configuration changes:
[ssh_connection]
pipelining = False
ssh_args = -o ControlMaster=auto -o ControlPersist=30m -o StrictHostKeyChecking=no

Ping Module:
ansible -i ec2.py ec2 -m ping

Create Instance 3-webserver and 1-dbserver
ansible-playbook -i ec2.py instance.yml

Verify ec2 instance ip address
./ec2.py --list --profile default --refresh-cache
ansible -i ec2.py --limit "tag_Name_webserver*" -m ping all


Setup or deployment code in webserver and install database in dbserver
ansible-playbook -i ec2.py deploy_playbook.yml
