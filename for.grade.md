```bash

###########################
## homework
ssh -i ~/.ssh/id_rsa.redhat -tt zhengwan-redhat.com@bastion.8e50.example.opentlc.com byobu

mkhomedir_helper zhengwan-redhat.com
yum -y install byobu

https://tower1.8e50.example.opentlc.com
admin  /  r3dh4t1!

vim /root/.ssh/mykey.pem
chmod 400 /root/.ssh/mykey.pem

ssh -i /root/.ssh/mykey.pem zhengwan-redhat.com@workstation-cba1.rhpds.opentlc.com

git clone https://github.com/wangzheng422/ansible_advance_homework

cd ansible_advance_homework
OSP_GUID=cba1

ansible-playbook site-setup-workstation.yml -e OSP_GUID=${OSP_GUID} --private-key=/root/.ssh/mykey.pem -u zhengwan-redhat.com

ssh -i /root/.ssh/openstack.pem cloud-user@workstation-${OSP_GUID}.rhpds.opentlc.com

https://tower1.8e50.example.opentlc.com
admin  /  r3dh4t1!

TOWER_GUID=8e50
OSP_GUID=cba1
OPENTLC_LOGIN=zhengwan-redhat.com
OPENTLC_PASSWORD=******
GITHUB_REPO=https://github.com/wangzheng422/ansible_advance_homework
JQ_REPO_BASE=http://www.opentlc.com/download/ansible_bootcamp
REGION=us-east-1
RH_MAIL_ID=zhengwan@redhat.com

ansible-playbook site-install-isolated-node.yml -e TOWER_GUID=${TOWER_GUID} -e OSP_GUID=${OSP_GUID} -e opentlc_login=${OPENTLC_LOGIN} -e path_to_opentlc_key=/root/.ssh/mykey.pem -e param_repo_base=${JQ_REPO_BASE} -e opentlc_password=${OPENTLC_PASSWORD} -e REGION_NAME=${REGION} -e EMAIL=${RH_MAIL_ID} -e github_repo=${GITHUB_REPO}

vi /root/.ssh/openstack.pem
# to remove the leading and endding line beginning with #

ansible-playbook site-config-tower.yml -e tower_GUID=${TOWER_GUID} -e osp_GUID=${OSP_GUID} -e opentlc_login=${OPENTLC_LOGIN} -e path_to_opentlc_key=/root/.ssh/mykey.pem -e param_repo_base=${JQ_REPO_BASE} -e opentlc_password=${OPENTLC_PASSWORD} -e REGION_NAME=${REGION} -e EMAIL=${RH_MAIL_ID} -e github_repo=${GITHUB_REPO}

cd 
mkdir ~/bin
wget http://www.opentlc.com/download/ansible_bootcamp/scripts/common.sh
wget http://www.opentlc.com/download/ansible_bootcamp/scripts/jq-linux64 -O ~/bin/jq
wget http://www.opentlc.com/download/ansible_bootcamp/scripts/order_svc.sh
chmod +x order_svc.sh ~/bin/jq common.sh

cat << EOF > credential.rc
export username=zhengwan-redhat.com
export password=***
export uri=https://labs.opentlc.com
EOF

source credential.rc ; ./order_svc.sh -y -c 'OPENTLC Automation' -i 'Ansible Advanced - Three Tier App' -t 1 -d 'dialog_expiration=7;region=na;nodes=1;dialog_runtime=8'

https://tower1.8e50.example.opentlc.com/
# to run job template to test

cd ansible_advance_homework
OSP_GUID=cba1
ANSIBLE_ADVANCE_GUID=8e50
ansible-playbook grading-script.yml -e OSP_GUID=${OSP_GUID} -e ANSIBLE_ADVANCE_GUID=${ANSIBLE_ADVANCE_GUID}

###########################
## 3 tier app
ssh -i ~/.ssh/id_rsa.redhat -tt zhengwan-redhat.com@bastion.d71e.example.opentlc.com byobu


#############################
## openstack
ssh -i ~/.ssh/id_rsa.redhat -tt zhengwan-redhat.com@workstation-cba1.rhpds.opentlc.com byobu

# wget http://www.opentlc.com/download/ansible_bootcamp/openstack_keys/openstack.pub

# cat openstack.pub  >> /home/cloud-user/.ssh/authorized_keys

# yum install -y python-pip git
# pip install openstacksdk ansible -U

# mkdir /etc/openstack
# cat << EOF > /etc/openstack/clouds.yaml
# clouds:
#   ospcloud:
#     auth:
#       auth_url: http://192.168.0.20:5000/
#       password: r3dh4t1!
#       project_name: admin
#       username: admin
#     identity_api_version: '3.0'
#     region_name: RegionOne
# ansible:
#   use_hostnames: True
#   expand_hostvars: False
#   fail_on_errors: True
# EOF

# ansible localhost -m os_auth -a cloud=ospcloud
# ansible localhost -m os_user_facts -a cloud=ospcloud


# cat << EOF > osp_image.yml
# - hosts: localhost
#   become: yes

#   tasks:
#   - name: Download RHEL image
#     get_url:
#       url: http://www.opentlc.com/download/osp_advanced_networking/rhel-guest-image-7.2-20151102.0.x86_64.qcow2
#       dest: /root/rhel-guest-image-7.2-20151102.0.x86_64.qcow2
#   - name: Load RHEL image into Glance
#     os_image:
#       cloud: ospcloud
#       name: rhel-guest
#       container_format: bare
#       disk_format: qcow2
#       state: present
#       filename: /root/rhel-guest-image-7.2-20151102.0.x86_64.qcow2
# EOF

# ansible-playbook osp_image.yml

# git clone https://github.com/prakhar1985/osp-ansible-lab.git
# cd osp-ansible-lab

# ansible-playbook site-osp-setup.yml




```