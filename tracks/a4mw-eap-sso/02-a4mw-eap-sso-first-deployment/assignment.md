---
slug: a4mw-eap-sso-first-deployment
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
🗃️ First deployment
===
#### Estimated time to complete: *10 minutes*<p>

BLAHBLAH


☑️ Task 1 - Locate and run the deploy Template
===

1. On the side navigation bar, under the **Resources** section, click on **Templates**
2. Click on the **sso-eap** template
3. On the page that opens, click the **Launch** button
4. The launch dialog open, asking for credentials (defaults are already set), click **Next**
5. Click **Launch**; you will be redirected the executing job output page.
6. Wait for the job to finish; you can scroll the output to have glimpse of what is being executed.



☑️ Task 2 - Verify the services are deployed
===




✅ Next Challenge
===
Press the `Check` button below to go to the next challenge once you’ve completed the task.


🐛 Encountered an issue?
====

If you have encountered an issue or have noticed something not quite right, please [open an issue](https://github.com/ansible-middleware/instruqt/issues/new?labels=a4mw-eap-sso&title=Issue+with+Deploy+Red+Hat+Single+Sign-On+with+Ansible+for+Middleware+collections+slug+ID:+a4mw-eap-sso-first-deployment&assignees=guidograzioli).

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
