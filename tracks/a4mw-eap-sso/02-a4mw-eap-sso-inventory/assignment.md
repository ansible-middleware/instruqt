---
slug: a4mw-eap-sso-inventory
id: ufntl6meghns
type: challenge
title: Inspecting an Inventory
teaser: Managing hosts and groups for our scenario
notes:

- type: text
  contents: |-
    # Inventories, create new inventory

    ![inventories-create-new-inventory.png](../assets/inventories-create-new-inventory.png)

    In this challenge, we will be creating a new inventory, adding hosts and creating a host group inside the inventory.
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
🗃️ Inventories
===
#### Estimated time to complete: *3 minutes*<p>

An inventory is a collection of hosts against which jobs (ex. playbooks) may be launched, the same as an Ansible inventory file, it indicates which nodes will be managed by the control machine, in this case the automation controller.

[Inventories](https://docs.ansible.com/automation-controller/latest/html/userguide/inventories.html) may be divided into *groups* and these groups contain the actual *hosts*. The *hosts* may be sourced manually or dynamically and can be referenced by their **IP addresses** or their **hostnames**.

In automation controller you will be able to run multiple playbooks against these inventories without recreating them.


☑️ Task 1 - Locate the Inventory
===

1. On the side navigation bar, under the **Resources** section, click on **Inventories**
2. Click on the **sso-eap** inventory
3. Click in the "**groups** tab item
4. Examine the groups configured in the inventory


☑️ Task 2 - Examine hosts in the inventory
===

1. If you are not in the **sso-eap** inventrory, click on it again to open it.
2. On the tab bar, click on **Hosts**
3. Examine the hosts configured in the inventory:
  * `jbcs-eap` will execute Jboss Core Services and Jboss Enterprise Application platform, and belongs to the `db`, `jbcs`, and `eap` groups
  * `sso1` and `sso2` will provide Single Sign-On, and belong to the `sso` group


✅ Next Challenge
===
Press the `Check` button below to go to the next challenge once you’ve completed the task.

🐛 Encountered an issue?
====

If you have encountered an issue or have noticed something not quite right, please [open an issue](https://github.com/ansible-middleware/instruqt/issues/new?labels=a4mw-eap-sso&title=Issue+with+Deploy+Red+Hat+Single+Sign-On+with+Ansible+for+Middleware+collections+slug+ID:+a4mw-eap-sso-inventory&assignees=guidograzioli).

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
