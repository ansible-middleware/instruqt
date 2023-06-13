---
slug: a4mw-eap-sso-first-deployment
id: ufntl6meghns
type: challenge
title: Our first deployment
teaser: Launching the job template to deploy JBCS and EAP services
notes:
- type: text
  contents: |-
    # Our first deployment

    In this challenge, now that the project setup is finalized, we will start our first deployment.

    ![job-output.png](../assets/job-output.png)
- type: text
  contents: |-
    # Scenario overview

    At the end of deployment, two services will be up and running on the `jbcs-eap` node:
    * JBCS is a web server and reverse proxy, accepting https requests and proxying down to EAP
    * EAP is an application container, running a custom java web application called *addressbook*

    ![scenario](../assets/scenario-1.png)
- type: text
  contents: |-
    # Addressbook web application

    This how the web application version 1.0.0, which we will be deploying in JBoss EAP, looks like:

    ![addressbook.png](../assets/addressbook.png)
tabs:
- title: Automation controller
  type: service
  hostname: control
  path: /
  port: 443
- title: Terminal
  type: terminal
  hostname: control
- title: JBCS-mcm
  type: service
  hostname: jbcs-eap
  path: /mcm/
  port: 443
- title: addressbook
  type: service
  hostname: jbcs-eap
  path: /addressbook/
  port: 443
difficulty: basic
timelimit: 600
---
🗃️ First deployment
===
#### Estimated time to complete: *15 minutes*<p>

Now that we are comfortable with the Ansible controller configuration, we can actually execute the very first playbook, which:

* Installs pre-requisite packages and resources on all hosts
* Installs JBoss Core Services on the **jbcs-eap** host
* Installs JBoss Enterprise Application Platform on the **jbcs-eap** host
* Deploys the **addressbook** web application on the JBoess EAP service

If not already, you can log in with the following credentials and then continue on to the tasks:

* Username: `admin`
* Password: `ansible123!`

☑️ Task 1 - Locate and run the deploy Template
===

1. On the side navigation bar, under the **Resources** section, click on **Templates**
2. Click on the **sso-eap-deploy** template
3. On the page that opens, click the **Launch** button
4. The launch dialog opens, on a **Survey** asking for credentials (defaults are already set), click **Next**
5. You are now presented with the Launch **Preview** page: click **Launch**. You will be redirected the executing job output page.
6. Wait for the job to finish; you can scroll the output to have glimpse of what is being executed.
7. Notice how each task output is colored differently; colors correspond to outcome status, which is very important in Ansible:
 * **OK (green)** indicates that no change was applied by tasks because the configuration was already found as expected.
 * **CHANGED (yellow)** indicates that the wanted configuration has been applied, thus generating a change.
 * **FATAL (red)** indicates that the tasks failed for some reason; sometimes the failure is fatal and the execution will stop; other times, showing **FAILED - TRYING (black)**, you will see the playbook recovers the situation. An example of recovery is when a playbook runs a command to check for the existance of some resource, and runs a create action when that command failed.
 * **SKIPPED (cyan)** indicates a tasks that was not executed, either because the playbook decided so, or because of some condition not allowing it run.


☑️ Task 2 - Noteworthy tasks
===

Let's inspect some tasks that run, producing the output at or around the following lines:

* Ensuring required rpm packages are present
  * line 11: use rpm to check installed packages
  * line 16: add any missing package (for each host) to a list
  * line 21: execute the package manager to install missing packages
* Download JBCS install zipfiles
  * line 131: contact the JBossnetwork API to find an authenticated download URL
  * line 137: perform the download
* Configure and install JBCS
  * line 149: extract zipfile
  * line 192: configure TLS/SSL
  * line 198: configure the reverse proxy
* Start and verify JBCS systemd unit
  * lines 210-232
* Download JBoss EAP install zipfiles
  * line 324: contact the JBossnetwork API to find an authenticated download URL
  * line 334: perform the download
  * line 401: contact the JBossnetwork API to find an authenticated download URL for the patch
  * line 414: perform the download of the cumulative patch
* Install JDBC postgresql module in JBoss EAP
  * line 620: download the library JAR
  * line 626: deploy the module
* Deploy the addressbook warfile
  * lines 757-758


☑️ Task 3 - Verify the services are deployed
===

1. On the window top bar, locate and click the **JBCS-mcm** tab
2. The page should show **mod_cluster/1.3.16.Final-10** in the heading. This means JBCS is operational; if it does not, try to click the ↻ 'refresh' button on the right side of the top bar
3. In page content, you should read in **Node jbcs-eap (ajp://127.0.0.1:8009):**. This means EAP is operational, and attached to JBCS modcluster (reverse proxy) facility.
4. Now on the top bar, locate and click the **addressbook** tab
5. Our sample web application should open, or if the page was already opened, it will show **Not found**; click the ↻ 'refresh' button on the right side of the top bar, and the application will be loaded in the browser.
6. If any of the above points fails for you, jump back to Task 1, and repeat the steps.


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
