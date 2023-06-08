---
slug: playbooks
id: tvbrekcox4wo
type: challenge
title: Create playbook
tabs:
- title: getting_started
  type: terminal
  hostname: getting-started-demo
  workdir: /home/getting_started/
difficulty: basic
timelimit: 600
---
Now lets use the below playbook.yml to use the wildfly collection and to deploy wildfly on the RHEL 8 machine.

```
---
- name: "Installation and configuration"
  hosts: localhost
  vars:
   wildfly_install_workdir: '/opt'
   install_name: "wildfly"
   wildfly_user: "{{ install_name }}"
   wildfly_config_base: standalone-ha.xml
   wildfly_version: "26.0.0.Final"
   wildfly_home: "{{ wildfly_install_workdir }}/{{ install_name }}-{{ wildfly_version }}"
  collections:
   - middleware_automation.wildfly
  tasks:
   - name: Include wildfly role
     ansible.builtin.include_role:
       name: middleware_automation.wildfly.wildfly_install
   - name: "Set up for Wildfly instance"
     include_role:
       name: middleware_automation.wildfly.wildfly_systemd
     vars:
       wildfly_config_base: 'standalone-ha.xml'
       wildfly_basedir_prefix: "/opt/{{ install_name }}"
       wildfly_config_name: "{{ install_name }}"
       wildfly_instance_name: "{{ install_name }}"
       service_systemd_env_file: "/etc/{{ install_name }}.conf"
       service_systemd_conf_file: "/usr/lib/systemd/system/{{ install_name }}.service"
```