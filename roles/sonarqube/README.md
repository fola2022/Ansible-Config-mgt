Role Name
=========
This role installs sonarqube 8. It's intended to be used inside a dockerfile as a POC of ansible based containers provisioning. Not to be used in production environments

Requirements
------------
Sonarqube needs a PostgreSQL database as it's data repository.

Role Variables
--------------
This role requires the following variables, with the default value as indicated:
```yaml
sonar_user:          sonar          # OS System user
sonar_version:       8.9.0.43852    # Sonar version

# DDBB Config
sonar_jdbc_username: sonar          # DDBB User name
sonar_jdbc_password: sonar          # DDBB Password
sonar_jdbc_host:     localhost      # DDBB Hostname
sonar_jdbc_port:     5432           # DDBB Port
sonar_jdbc_ddbb:     sonardb        # DDBB Name
```

Dependencies
------------
None

Example Playbook
----------------
Register the role in requirements.yml:
```yaml
- src: capitanh.sonar_ansible_role
  name: sonar
```
Include it in your playbooks:
```yaml
- hosts: servers
  roles:
  - sonar
```

License
-------
BSD
