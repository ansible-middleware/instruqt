---
slug: a4mw-eap-sso-collections
id: jabxfy1rqlke
type: challenge
title: Collections to the rescue
teaser: Import the Red Hat SSO collection and deploy an HA cluster
notes:
- type: text
  contents: |-
    # Ansible for Middleware collections

    Our latest deployment left us with a non-functional application. We already used the Red Hat EAP and JBCS collections, let's see if we can
    find something else that can help us:

    ![hub-collections.png](../assets/hub-collections.png)

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
- title: JBCS-mcm
  type: service
  hostname: jbcs-eap
  path: /mcm/
  port: 443
- title: SSO-console
  type: service
  hostname: jbcs-eap
  path: /auth/
  port: 443
difficulty: basic
timelimit: 600
---
 💡 Single Sign-On deployment
===
#### Estimated time to complete: *30 minutes*<p>


☑️ Task 1 - Load the repository directory in the editor
===

1. Go to the **editor** tab, clicking on the link in topbar; if the git repository is still open from the previous challenge, proceed to Task 2 below.
2. In the **editor** tab, click on the File menu, then **Load directory**
3. Select the **eap-sso** directory, which is the working copy of the git repository
4. Click **OK** and then confirm in the dialog that open, that you trust the contents


☑️ Task 2 - Add a Single Sign-On playbook
===

1. In the editor page, make sure you are in the EXPLORER view, by pressing **Ctrl-Shift-E** or clicking on the first button on the left button bar.
2. Click **File** menu, then **New File..**
3. In the dialog that opens, type **sso.yml**, **Enter**
4. Make sure the path is **/home/rhel/eap-sso/sso.yml** and click **OK**
5. You should have now an empty file editor tag, named **sso.yml**
6. Paste the following contents:
```
---
- name: Playbook for rhsso Hosts
  hosts: sso
  become: true
  roles:
    - role: redhat.sso.sso
      sso_admin_password: "redhat1!but12long"
```
   The playbook above does nothing else than invoking the main **sso** install role of the **redhat.sso** collection. We pass a parameter just under the role, `sso_admin_password` variable, in that way and not in the group_vars, because for added security, the collection **does NOT** provide a default for the administrator password, and forces the user to define one (a strong one). Generally, you would not type the parameter value `redhat1!but12long` here, but rely on some encryption secret management facility instead, like Ansible vaults. However, this is out of the scope of this workshop, and we will leave that to you.
7. Type **Ctrl-S** to save, or use the **File**/**Save** menu
8. Locate the **deploy.yml** file, and click to open it in a new editor tab
9. To add the newly create playbook in the main playbook, on line 6 (after jbcs.yml and before eap.yml), type:
```
- import_playbook: sso.yml
```
10. Type **Ctrl-S** to save, or use the **File**/**Save** menu

Ok, we now have the playbooks in; let's configure the collection in the next challenge.


☑️ Task 3 - Config Single Sign-On group variables
===

1. In the editor page, make sure you are in the EXPLORER view, by pressing **Ctrl-Shift-E** or clicking on the first button on the left button bar.
2. In the EXPLORER panel, expand the **inventory/group_vars** directory, and right-click on **group_vars**
3. In the context menu, choose **New file** and type **sso.yml** followed by **Enter** key
4. You will be presented with a new editor tab; paste the following in it:
```
---
# install settings
sso_offline_install: False

# ha cluster settings
sso_ha_enabled: True
sso_remote_cache_enabled: False
sso_jgroups_subnet: "{{ (ansible_default_ipv4.address | default(ansible_all_ipv4_addresses[0])) + '/24' }}"

# network settings
sso_configure_firewalld: True
sso_http_port: 8081
sso_management_port_bind_address: 0.0.0.0
sso_modcluster_url: "jbcs-eap"

# database settings
sso_jdbc_engine: postgres
sso_jdbc_url: "{{ site_jdbc_url }}/keycloak"
sso_db_user: keycloak-user
sso_db_pass: keycloak-pass
sso_db_background_validate_on_match: True
sso_db_valid_conn_sql: 'SELECT 1'

admin_pass: "redhat1!but12long"
```

7. Type **Ctrl-S** to save, or use the **File**/**Save** menu

We now have all configuration we need to pass to the **redhat.sso** collection for installing Red Hat Single Sign-On; let's discuss the variable briefly:

* `sso_offline_install`: `False` here we tell the collection we want to download install files from the Customer Portal. When set to true, it instructs the collection to look for local files instead, useful when exeuting deployments without outbound Internet access in security enforced areas.
* `sso_ha_enabled` and `sso_remote_cache_enabled`: we tell the collection that we are deploying an HA cluster, without using an external cache service (which could be implemented by Red Hat DataGrid, we have a certified collection, **redhat.data_grid**, that integrates that too!).
* `sso_jgroups_subnet`: we tell the subnetwork to group instances for the cluster; this is usually not necessary, but the Instruqt environment has some network settings that require it.
* `sso_configure_firewalld`, `sso_http_port`: we tell the collection to configure **firewalld** for us, and that we want to run http on the non-default port 8081 (default is 8080)
* `sso_modcluster_url`: this is the hostname of the JBCS service; Single Sign-On will use the same instance for reverse proxy
* the remaining are database settings which should be self-explanatory


☑️ Task 4 - Commit changes
===

1. Switch to the **Source Control** git dialog (third icon on the left column, should have a blue notification)
2. Fill the dialog text called **Message** with `Add SSO playbook`
3. Click on the blue **Commit** button to apply the changes. You will notice that while the editor suggests to synchronize changes (ie. a git push) to the remote repository, however this operation is not necessary for our workshop.


☑️ Task 5 - Locate and run the deploy Template
===

1. Switch to the **Automation controller** tab
2. On the side navigation bar, under the **Resources** section, click on **Templates**
3. Click on the **sso-eap-deploy** template
4. On the page that opens, click the **Launch** button
5. The launch dialog opens the **Survey**, asking for credentials (defaults are already set), click **Next**
6. Click **Launch**; you will be redirected the executing job output page.

If not logged in or your session expired, you can login with the following credentials and then continue on to the tasks:

* Username: `admin`
* Password: `ansible123!`


☑️ Task 5 - Validate deployment
===

1. Follow the job execution output up to the end
2. Note that all former tasks should be ok (green) or skip (cyan), except now there will be a whole new playbook running, starting around line 199.
3. Notice how the playbook is running simultaneously against the two **sso1** and **sso2** hosts this time.
4. Note, around line 508, how the restart of the SSO nodes is not simultaneous; instead, they are serially restarted to provide no-downtime cluster restarts
4. On the window top bar, locate and click the **JBCS-mcm** tab
5. The page should show **mod_cluster/1.3.16.Final-10** in the heading. This means JBCS is operational; if it does not, try to click the ↻ 'refresh' button on the right side of the top bar
6. In page content, you should read in **Node sso1 (ajp://a.b.c.d:8009):** and **Node sso2 (ajp://a.b.c.d:8009):**. This means SSO is operational, and attached to JBCS modcluster (reverse proxy) facility.
7. On the window top bar, locate and click the **SSO-console** tab, and click the ↻ 'refresh' button on the right side of the top bar
8. You should be presented with the SSO frontpage



✅ Next Challenge
===
Press the `Check` button below to go to the next challenge once you’ve completed the task.

🐛 Encountered an issue?
====

If you have encountered an issue or have noticed something not quite right, please [open an issue](https://github.com/ansible-middleware/instruqt/issues/new?labels=a4mw-eap-sso&title=Issue+with+Deploy+Red+Hat+Single+Sign-On+with+Ansible+for+Middleware+collections+slug+ID:+a4mw-eap-sso-collections&assignees=guidograzioli).

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
