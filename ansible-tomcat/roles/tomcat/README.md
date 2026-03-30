# tomcat role

## Description
Setup Tomcat 11 from Apache tarball and manage systemd service.

## Role variables
Defined in `roles/tomcat/defaults/main.yml`:
- `tomcat_version`
- `tomcat_user`
- `tomcat_group`
- `tomcat_install_dir`
- `tomcat_service_name`
- `tomcat_archive_url`
- `tomcat_archive_dest`
- `tomcat_service_file`
- `tomcat_java_pkg`
- `tomcat_app_war`
- `tomcat_app_source`
- `tomcat_app_dest`

## Example playbook
```yaml
- hosts: all
  become: yes
  roles:
    - tomcat
```

## Inventory
Use YAML inventory `ansible-tomcat/hosts.yml` in root directory:
```yaml
all:
  hosts:
    vm-alpha:
      ansible_host: 35.241.224.131
    vm-beta:
      ansible_host: 34.38.123.95
    vm-gamma:
      ansible_host: 35.205.215.122
```
