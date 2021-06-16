# Hadoop-ansible
- Installs Hadoop cluster with ansible on RHEL 7

## Before Install
- Download hadoop installable and place it in a folder 
- Ensure a passwordless SSH is setup between all the hosts in the cluster for the {GENERIC_USER}
- Ensure {GENERIC_USER} has permissions to create folders under the path mentioned by varibale {HADOOP_PATH}
- Modify hosts/host with host names of the cluster
- Update vars/var_basic.yml for {DOWNLAOD_PATH}, {PATH_TO_PYTHON_EXE}, {HADOOP_PATH}
- Update {PATH_TO_PYTHON_EXE} in ansible.cfg, roles/hadoop/tasks/main.yml
- Update {MASTER_IP}, {MASTER_HOSTNAME} in vars/var_master.yml, vars/var_workers.yml
- Update {GENERIC_USER}, {GENERIC_USER_GROUP} in vars/user.yml

## Install Hadoop

1. Download Hadoop to any path
2. Update the {{ download_path }} and {{ hadoop_version }} in vars/var_basic.yml
```
download_path: "{DOWNLAOD_PATH}" # your local path 
hadoop_version: "3.0.0" # your hadoop version
hadoop_path: "{HADOOP_PATH}" # default in user "hadoop" home
hadoop_config_path: "/home/hadoop/hadoop-{{hadoop_version}}/etc/hadoop"
hadoop_tmp: "/home/hadoop/tmp"
hadoop_dfs_name: "/home/hadoop/dfs/name"
hadoop_dfs_data: "/home/hadoop/dfs/data"

```

### Install Master

run shell like

```
ansible-playbook -i hosts/host master.yml
```

### Install Workers


run shell like:
```
master_ip:  your hadoop master ip
master_hostname: your hadoop master hostname

above two variables must be same like your real hadoop master

ansible-playbook -i hosts/host workers.yml -e "master_ip=172.16.251.70 master_hostname=hadoop-master"

```

