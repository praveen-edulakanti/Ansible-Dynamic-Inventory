# Ansible-Dynamic-Inventory
Download these ec2.ini and ec2.py files to the your project folder:<br/>
wget https://raw.githubusercontent.com/ansible/ansible/devel/contrib/inventory/ec2.py   <br/>
wget https://raw.githubusercontent.com/ansible/ansible/devel/contrib/inventory/ec2.ini

To test if everything is good, try executing the ec2.py by listing your resources:<br/>
./ec2.py --list


/etc/ansible/ansible.cfg configuration changes:<br/>
[ssh_connection] <br/>
pipelining = False <br/>
ssh_args = -o ControlMaster=auto -o ControlPersist=30m -o StrictHostKeyChecking=no <br/>

Ping Module: <br/>
ansible -i ec2.py ec2 -m ping<br/>

Create Instance 3-webserver and 1-dbserver<br/>
ansible-playbook -i ec2.py instance.yml

Verify ec2 instance ip address<br/>
./ec2.py --list --profile default --refresh-cache<br/>
ansible -i ec2.py --limit "tag_Name_webserver*" -m ping all


Setup or deployment code in webserver and install database in dbserver<br/>
ansible-playbook -i ec2.py deploy_playbook.yml
