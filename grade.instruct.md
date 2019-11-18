github: https://github.com/wangzheng422/ansible_advance_homework

tower id: 8e50
openstack id: cba1
3 tier app id: 11b9
```bash

###########################
## homework
# first login to base
ssh -i ~/.ssh/id_rsa.redhat -tt zhengwan-redhat.com@bastion.8e50.example.opentlc.com byobu

# if no home directory, create one.
mkhomedir_helper zhengwan-redhat.com
# install tmux/screen enhancement for great firewall case
yum -y install byobu

# login to ansible tower to check
https://tower1.8e50.example.opentlc.com
admin  /  r3dh4t1!

# check and change the key file mode
vim /root/.ssh/mykey.pem
chmod 400 /root/.ssh/mykey.pem

# test the key file can be used to connec to openstack
ssh -i /root/.ssh/mykey.pem zhengwan-redhat.com@workstation-cba1.rhpds.opentlc.com

# under home dir, clone my git repository
git clone https://github.com/wangzheng422/ansible_advance_homework

# go to git dir and prepare the env
cd ansible_advance_homework
OSP_GUID=cba1

ansible-playbook site-setup-workstation.yml -e OSP_GUID=${OSP_GUID} --private-key=/root/.ssh/mykey.pem -u zhengwan-redhat.com

# check you can connect to openstack
ssh -i /root/.ssh/openstack.pem cloud-user@workstation-${OSP_GUID}.rhpds.opentlc.com

# check on the ansible tower again
https://tower1.8e50.example.opentlc.com
admin  /  r3dh4t1!

# install the isolated node
TOWER_GUID=8e50
OSP_GUID=cba1
OPENTLC_LOGIN=zhengwan-redhat.com
OPENTLC_PASSWORD=******
GITHUB_REPO=https://github.com/wangzheng422/ansible_advance_homework
JQ_REPO_BASE=http://www.opentlc.com/download/ansible_bootcamp
REGION=us-east-1
RH_MAIL_ID=zhengwan@redhat.com

ansible-playbook site-install-isolated-node.yml -e TOWER_GUID=${TOWER_GUID} -e OSP_GUID=${OSP_GUID} -e opentlc_login=${OPENTLC_LOGIN} -e path_to_opentlc_key=/root/.ssh/mykey.pem -e param_repo_base=${JQ_REPO_BASE} -e opentlc_password=${OPENTLC_PASSWORD} -e REGION_NAME=${REGION} -e EMAIL=${RH_MAIL_ID} -e github_repo=${GITHUB_REPO}

# to remove the leading and endding line beginning with #
# this is for some special cases
vi /root/.ssh/openstack.pem

# config tower
ansible-playbook site-config-tower.yml -e tower_GUID=${TOWER_GUID} -e osp_GUID=${OSP_GUID} -e opentlc_login=${OPENTLC_LOGIN} -e path_to_opentlc_key=/root/.ssh/mykey.pem -e param_repo_base=${JQ_REPO_BASE} -e opentlc_password=${OPENTLC_PASSWORD} -e REGION_NAME=${REGION} -e EMAIL=${RH_MAIL_ID} -e github_repo=${GITHUB_REPO}

# login to tower to run the ci-cd job 
https://tower1.8e50.example.opentlc.com/
# to run job template to test

# run the grading ansible playbook
cd ansible_advance_homework
OSP_GUID=cba1
ANSIBLE_ADVANCE_GUID=11b9
ansible-playbook grading-script.yml -e OSP_GUID=${OSP_GUID} -e ANSIBLE_ADVANCE_GUID=${ANSIBLE_ADVANCE_GUID}

```