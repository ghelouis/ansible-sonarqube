# [Ansible](https://www.ansible.com/overview/how-ansible-works) playbook for setting up a [SonarQube](https://docs.sonarqube.org/latest/) instance

This is an attempt to automate the official setup process as per described [here](https://docs.sonarqube.org/latest/setup/install-server/).

## Server pre-requisite
* Tested on Ubuntu 18.04, but should work on any distrib using `apt`
* Official hardware [recommendations](https://docs.sonarqube.org/latest/requirements/requirements/)
* SSH root access

## Overview
This will be installed:
- PostgreSQL
- SonarQube itself (java app)
- Nginx reverse proxy

## Operate
Sonar gets installed as a systemd daemon.
- Logs: `journalctl -fu sonarqube`
- Stop: `systemctl stop sonarqube`
- Start: `systemctl start sonarqube`

## Run
- `ansible-playbook -i hosts setup-sonar.yml --vault-password-file ~/.vault_pass.txt`
Setting up a [vault](https://docs.ansible.com/ansible/latest/user_guide/playbooks_vault.html#single-encrypted-variable)
is easy and makes it possible to avoid using clear text passwords.

## Vars
- sonar_system_user: the linux user that will operate SonarQube
- sonar_db_user: the postgres user/owner of the database
- sonar_db_name: the postgres database name
- sonar_db_password: the postgres user's password, use ansible vault to
avoiding setting a clear text value

## Resources
- [PostgreSQL User Module](https://docs.ansible.com/ansible/latest/modules/postgresql_user_module.html)
- [PostgreSQL DB Module](https://docs.ansible.com/ansible/latest/modules/postgresql_db_module.html)

## TODO
- Implement Linux platform notes as per documented [here](https://docs.sonarqube.org/latest/requirements/requirements/)
