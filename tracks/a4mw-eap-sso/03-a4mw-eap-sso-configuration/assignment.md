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

    Now that base services are deployed, we will stop a minute and fire up the source code editor, in order to take a look at the Ansible resources which allowed us to successfully execute our operations

    ![editor](../assets/editor.png)
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

**Note**: in the editor source pages, sometimes the code linter may underline some code in red, and show the error: `the role '<namespace.collection.role>' was not found in <a.list.of.paths> ansible-lintsyntax-check[specific]`. It seems the linter is confused by the fact collections are not installed in the control machine, but in the Ansible controller service. Those errors can be completely ignored.


☑️ Task 1 - Load the repository directory in the editor
===

1. In the **editor** tab, click on the **File** menu, then **Open folder...**
2. Select the **eap-sso** directory, which is the working copy of the git repository
3. Click **OK** and then confirm in the dialog that opens, that you trust the contents, by clicking the **Yes, I Trust the authors** button
4. Note the project directory will populate the EXPLORER panel on the left side


☑️ Task 2 - Inspect the JBCS playbook and variables
===

1. Find the file **jbcs.yml** in the project _EXPLORER_ (directory tree on the left side)
2. Note where the playbook invokes the collection `jbcs` role at line 7
```
  roles:
    - middleware_automation.jbcs.jbcs
```
3. Take a look at preliminary steps in the `pre_tasks` section: those operations do some selinux configuration, ie. allowing the JBCS service to open proxied ports and allowing to execute with NIS (Network Information Service). This is an example of configuration that is currently required in the playbook, but will eventually be taken care of by the **redhat.jbcs** collection in a future release, since its directly related to the JBCS service running on RHEL.
4. Find the file **inventory/group_vars/jbcs.yml** in the directory tree. The variables defined in this file will override the collection defaults.


☑️ Task 3 - Inspect the EAP playbook and variables
===

1. Find the file **eap.yml** in the directory tree
2. Note where the playbook invokes the collection roles at line 5. In this case, we invoke three different roles, to setup the JDBC driver module in EAP and the systemd unit, in addition to the main install operation.
  ```
    roles:
      - redhat.eap.eap_install
      - redhat.eap.eap_driver
      - redhat.eap.eap_systemd
  ```
3. Take a look at preliminary steps in the `pre_tasks` section: those operations setup the instance firewall to allow ingress to ports use by EAP
4. Find the file **inventory/group_vars/eap.yml** in the directory tree; the variables defined in this file will override the collection defaults, worth noting that:
  * `app_url` is the download URL of the web application we deploy in EAP
  * `eap_yml_configs` loads additional configuration in EAP, specified in the YAML file
5. Find the file **templates/eap_ymlconfig.yml.j2** in the directory tree
  * This file contains configuration that is applied to EAP subsystems; declarative configuration of EAP components during its bootstrap phase is a new feature which has been made available, in Techincal Preview, since Wildfly 26.0.1/JBoss EAP 7.4.5, and will be Generally Available in the upcoming EAP 8.0. The module providing the feature is called **YAML Configuration Extension**, and the **redhat.eap** collection provides both the automatic install for the cumulative patch version needed (switch back to the **inventory/group_vars/eap.yml** file) via the `eap_apply_cp` variable, and the steps to enable it via the `eap_enable_yml_config` variable. Also, note that when `eap_apply_cp` is set to `True`, it is possible to pass the collection a specific patch version (like, for instance, `eap_patch_version: 7.4.7`) to be applied; otherwise, letting the variable undefined instructs the collection to determine what is the most recent patch version released at the time of execution.



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
