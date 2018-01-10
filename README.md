Ansible playbooks to deploy highly available sensu infrastructure

# Prerequisites
* Servers/VMs are pre installed with RHEL 7
* Servers/VMs are configured with ssh keys and keyless ssh from the ansible host
* Rabbitmq VMs are configured with keyless ssh between them
* RHEL 7 yum repos are setup and accessible
* DNS or hosts files are configured for name resolution(critical for rabbitmq cluster)
* Firewall ports are opened between target servers being monitored and Sensu infrastructure
* Firewall ports are opened between uchiwa dashboard and users 
* Local MTA postfix is configured to send emails from sensu servers for alerts
# Package versions

|Package           |Version      |Ports                                                     |
|------------------|-------------|----------------------------------------------------------|
|Redis + Sentinel  |3.2.10       |TCP 6379/26379                                            |
|Rabbitmq          |3.6.9        |TCP 5672/25672/4369                                       |
|HAproxy           |1.5.18       |TCP 5670-rabbitmq, 4567-sensu-api, 3000-uchiwa, 8080 stats|
|Keepalived        |1.3.9        |                                                          |
|Sensu server      |1.2.0-1      |                                                          |
|Sensu clients     |0.23.2-3     |                                                          |
|Sensu API         |1.2.0-1      |TCP 4567                                                  |
|Uchiwa            |1.1.0        |TCP 3000                                                  |


# How to run
To run playbooks first update the group_vars/all with environment specific parameters.
Then run the playbooks in the playbooks folder to deploy individual components or all
at the same time. Each components can be deployed on their own. There are playbooks to
deploy as well as remove as this will help in testing.

Following shows deploying just rabbitmq
```
ansible-playbook playbooks/install_rabbitmq.yaml
```
# To Do
* Add options to install packages from a local folder for offline environments.
* Add tests to verify components are installed/removed properly.
