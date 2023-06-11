---
slug: a4mw-eap-sso-configuration
id: 1okbglrcvrxi
type: challenge
title: Inspect the deployment configuration
teaser: Let's take a look at the Ansible resources which allowed us to deploy the
  services
notes:
- type: text
  contents: |-
    # Configuration

    ![projects-list-all.png](../assets/projects-list-all.png)

    .
tabs:
- title: Automation controller
  type: service
  hostname: control
  path: /
  port: 443
- title: Terminal
  type: terminal
  hostname: control
- title: editor
  type: service
  hostname: control
  path: /editor/
  port: 443
difficulty: basic
timelimit: 600
---
 💡 Configuration
===
#### Estimated time to complete: *5 minutes*<p>



Before you start with tasks below, switch to the **editor** tab in the top menu. You can always switch back and forth between the **Automation controller** and **editor** tabs
in case you want to compare the configuration from the two different prespectives.


☑️ Task 1 - Load the repository directory in the editor
===

1. In the **editor** tab, click on the File menu, then **Load directory**
2. Select the **eap-sso** directory, which is the working copy of the git repository
3. Click **OK** and then confirm in the dialog that open, that you trust the contents


☑️ Task 2 - Inspect the JBCS playbook and variables
===

1. Find the file **jbcs.yml** in the directory tree
2. Notice the collection call at
```
  roles:
    - middleware_automation.jbcs.jbcs
```
3. Take a look at preliminary steps in the `pre_tasks` section: those operations do some selinux
4. Find the file **inventory/group_vars/jbcs.yml** in the directory tree
5. The variables defined in this file will override the collection defaults


☑️ Task 3 - Inspect the EAP playbook and variables
===

1. Find the file **eap.yml** in the directory tree
2. Notice the collection calls at
```
  roles:
    - redhat.eap.eap_install
    - redhat.eap.eap_driver
    - redhat.eap.eap_systemd
```
  In this case, we invoke three different roles, to setup the JDBC driver module in EAP and the systemd unit, in addition to the main install operation.
3. Take a look at preliminary steps in the `pre_tasks` section: those operations setup the instance firewall to allow ingress to ports use by EAP
4. Find the file **inventory/group_vars/eap.yml** in the directory tree
5. The variables defined in this file will override the collection defaults:
  * `app_url: https://github.com/ansible-middleware/addressbook/releases/download/1.0.7/addressbook.war` is the web application we deploy in EAP
  * `eap_yml_configs: [ eap_ymlconfig.yml.j2 ]` load additional configuration in EAP, specified in the YAML file
6. Find the file **templates/eap_ymlconfig.yml.j2** in the directory tree
7. This file contains configuration that is applied to EAP subsystems.



✅ Next Challenge
===
Press the `Check` button below to go to the next challenge once you’ve completed the task.

🐛 Encountered an issue?
====

If you have encountered an issue or have noticed something not quite right, please [open an issue](https://github.com/ansible-middleware/instruqt/issues/new?labels=a4mw-eap-sso&title=Issue+with+Deploy+Red+Hat+Single+Sign-On+with+Ansible+for+Middleware+collections+slug+ID:+a4mw-eap-sso-configuration&assignees=guidograzioli).

<style type="text/css" rel="stylesheet">
  .lightbox {
    display: none;
    position: fixed;
    justify-content: center;
    align-items: center;
    z-index: 999;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    padding: 1rem;
    background: rgba(0, 0, 0, 0.8);
    margin-left: auto;
    margin-right: auto;
    margin-top: auto;
    margin-bottom: auto;
  }
  .lightbox:target {
    display: flex;
  }
  .lightbox img {
    /* max-height: 100% */
    max-width: 60%;
    max-height: 60%;
  }
  img {
    display: block;
    margin-left: auto;
    margin-right: auto;
  }
  h1 {
    font-size: 18px;
  }
    h2 {
    font-size: 16px;
    font-weight: 600
  }
    h3 {
    font-size: 14px;
    font-weight: 600
  }
  p span {
    font-size: 14px;
  }
  ul li span {
    font-size: 14px
  }
</style>
