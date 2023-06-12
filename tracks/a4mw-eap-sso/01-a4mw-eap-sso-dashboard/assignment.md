---
slug: a4mw-eap-sso-dashboard
id: bmibb5exppag
type: challenge
title: Exploring the web-UI and Dashboard
teaser: Let's explore the dashboard, inventory and projects!
notes:
- type: text
  contents: |-
    # Welcome to the Ansible for Middleware workshop

    In this interactive workshop we will demonstrate how easy it is to use Ansible Automation Platform and the A4MW collections to setup complex environments, perform deployments,
    and operate day 0-1-2 tasks.

    In the first part will be on Ansible automation controller, the web-based UI interface for **Red Hat Ansible Automation Platform**.
- type: text
  contents: |-
    # Ansible automation controller

    Meet Ansible automation controller, the web-based UI interface for **Red Hat Ansible Automation Platform**.

    Let's explore the web-UI interface, in order to get comfortable with what is already configured in.
- type: text
  contents: |-
    # Automation controller Projects

    ![projects-list-all.png](../assets/projects-list-all.png)

    The Dashboard view begins with a summary of your hosts, inventories, and projects. Each of these is linked to the corresponding objects for easy access.
- type: text
  contents: |-
    # Automation controller Jobs view

    ![ug-dashboard-jobs-view.png](../assets/ug-dashboard-jobs-view.png)

    Access the Jobs view by clicking Jobs from the left navigation bar. This view shows all the jobs that have ran, including projects, templates, management jobs, SCM updates, playbook runs, etc.
- type: text
  contents: |-
    # Automation controller Inventories view

    ![inventories-home-with-examples.png](../assets/inventories-home-with-examples.png)

    Access the Inventories view by clicking Inventories from the left navigation bar. This view shows all the inventories that are configured.

    An Inventory is a collection of hosts and groups against which jobs may be launched, the same as an Ansible inventory file.
- type: text
  contents: |-
    # Automation controller Job Templates view

    ![job-templates-home-with-example-job-template.png](../assets/job-templates-home-with-example-job-template.png)

    Access the Templates view by clicking Templates from the left navigation bar. This view shows all the templates that are configured.
tabs:
- title: Automation controller
  type: service
  hostname: control
  path: /
  port: 443
- title: Terminal
  type: terminal
  hostname: control
difficulty: basic
timelimit: 600
---
👋 Introduction to automation controller
===
#### Estimated time to complete: *5 minutes*<p>

Automation controller, formerly known as Ansible Tower, allows users of Red Hat Ansible Automation Platform to define, operate, scale, and delegate automation across their enterprise through a web-based UI or API.

The screen on the left shows the login screen. You can log in with the following credentials and then continue on to the tasks:

* Username: `admin`
* Password: `ansible123!`

☑️ Task 1 - Explore the Dashboard
===

Explore the Dashboard view.  Currently the Dashboard wont show much information since it has just been deployed, but you will be able to visit again once you finished the lab and notice the difference.

You will find the following buttons:

* Hosts
  The virtual machines that can be managed by Automation controller
* Failed hosts
  Virtual machines that are added to Automation controller, but cannot be accessed
* Inventories
  Groupings of hosts that can be targeted by Ansible playbooks / Job Templates
* Inventory sync fail
  Jobs that synchronize Host state with Inventory state that failed
* Projects
  Groups of ansible playbooks that are hosted in the same scm repository
* Projects sync fail
  Jobs that synchronize scm state with Projects state that failed


☑️ Task 2 - Explore the Inventories section
===

An **Inventory** is a collection of hosts against which playbooks may be launched, the same as an Ansible inventory file you might know from working with Ansible on the command line.

Click on the **Inventories** button in the Dashboard or the link in the sidebar menu and explore the **eap-sso** inventory that comes pre-loaded. Don't forget to look at the tabs!

In particular, the **Sources** tab page will list the inventories that are dinamically loaded from the project files. Open the **eap-sso-source** item and verify that its *Inventory file* option
points to the `inventory/inventory` file inside the **eap-sso** project.

Now click the **Sync** button: this will start the syncing between the hosts available to Ansible controller and those defined in the project git repository inventory. You will notice the field *Last Job Status* now reports **Pending** status, and after a few seconds **Running**; and eventually it will report **Successful** after the execution terminates. You can click on the **Pending** link to
access the output log of the synchonize operation: if you do, remember to go back to **eap-sso-source** inventory source page before going further ahead.

When the syncing is completed, on the tab bar, now click on **Back to Sources**, then the **Hosts** tab, and examine the hosts configured in the inventory:
  * `sso1` and `sso2` will provide the Single Sign-On authentication service, and belong to the `sso` group. The instances are up, but nothing else has been configured.
  * `jbcs-eap` will execute JBoss Core Services and JBoss Enterprise Application platform. Click on it, then switch to the **Groups** tab and verify it belongs to the `db`, `jbcs`, and `eap` groups.

A group is a set of hosts that facilitates sharing common variables across hosts: for instance, variables that apply to hosts providing the same service, like **eap**; or hosts that are located in the same environment, like **staging**; or even hosts that are located in the same place, **us-east-1** or **datacenter1** are good examples. Click on the **eap** group and check the **Details** page that opens: the variables shown are the values that have been fetched and synchronized by the job we just launched, and originate from scm repository that we will see in the next Task.


☑️ Task 3 - Explore the Projects section
===

**Projects** are logical groups of Ansible playbooks in automation controller. These playbooks usually reside in a source code version control system like Git (and platforms as GitHub or GitLab). With **Projects** we can reference a repository or directory with one or several playbooks, that we will later use.

Go back to Dashboard view and click on the **Projects** button, or click the link in the sidebar menu, and explore the **eap-sso** Project. The important settings in this configuration page are:

* *Source Control URL*: the Project is bound to a git repository called **eap-sso** located in the home directory for the _rhel_ user of the _control_ host.
* *Update revision on launch*: setting this instructs the Ansible controller to verify if new commits are available in the git repository every time the template associated with Project is executed.


☑️ Task 4 - Explore the Job Templates section
===

**Job Templates** are execution configurations, same concept as Ansible playbook.

Click on the **Templates** link in the sidebar menu and explore the **eap-sso-deploy** job template that comes pre-loaded. You will notice that it points to `deploy.yml` playbook inside the git repository
provided by the **eap-sso** project we have inspected in _Task 3_; in the next track sections we will use a code editor to open that git repository, make changes, and run new deployments using this job template.

If you click on the **Survey** tab, you'll find a pair of credentials which are configured to be set at every execution (do not mind the values, they have been set and encrypted by default): those enable the Ansible Middleware collection to perform downloads from the Red Hat Customer Portal automatically via a feature called **JBoss Network Download API**. Surveys are an important feature
of Ansible controller because they allow to manage variables, possibly secrets, which are not good enough candidates for ansible vault files, or external secret management services which
do not depend on the user that executes the deployment.


✅ Next Challenge
===
Press the `Next` button below to go to the next challenge once you’ve completed the tasks.

🐛 Encountered an issue?
====

If you have encountered an issue or have noticed something not quite right, please [open an issue](https://github.com/ansible-middleware/instruqt/issues/new?labels=a4mw-eap-sso&title=Issue+with+Deploy+Red+Hat+Single+Sign-On+with+Ansible+for+Middleware+collections+slug+ID:+a4wm-eap-sso-dashboard&assignees=guidograzioli).

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
