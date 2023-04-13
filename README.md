### Playbook to deploy Apache Airflow in cluster configuration on multiple servers with CeleryExecutor:

#### Playbook structure

```
├── inventories                 <- Dir with the inventories
│   ├── group_vars
│   │   └── all.yaml            <- Vars for deploy (connections, ports, etc)
│   └── hosts.yaml              <- List of hosts and ansible user/password
│
├── playbooks
│   └── main.yml                <- The main playbook consists of three roles
│
├── roles
│   ├── common                  <- Create dirs on target hosts, fill .env template for Airflow configuration
│   │   ├──tasks
│   │   │   ├── main.yml
│   │   │   └── run_airflow_container.yml
│   │   └──templates
│   │       └── airflow.env.j2
│   ├── servers                 <- Run containers for webserver, scheduler, flower, initiate db 
│   │   └──tasks
│   │       └── main.yml
│   └── workers                 <- Run containers for workers
│       └──tasks
│           └── main.yml
├── ansible.cfg                 <- ansible config file
└── README.md
```

#### Usage

1. **The playbook only deploys airflow on the specified servers, but does not prepare the infrastructure itself. Therefore, make sure that you have running servers to which you can connect via ssh under the user specified in the hosts, make sure that the database server and redis are also running.**
2. **Fill connections params in the *../group_vars/all.yml* either via env variables or manually**
3. **Run palybook**
```sh
ansible-playbook playbooks/main.yml -i inventories/hosts -v
```
4. **Set up the synchronization of dags with the git in any way convenient for you**

#### Result
![](./Airflow.drawio.png)
