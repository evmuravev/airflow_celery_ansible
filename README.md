Playbook to run airflow in cluster configuration on multiple servers with CeleryExecutor:
```sh
ansible-playbook playbooks/main.yml -i inventories/hosts -v -e @vars/main.yml
```
