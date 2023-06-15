---
slug: a4mw-eap-sso-auth-realm
id: rrqhy3aunpvs
type: challenge
title: Configuring Single Sign-On
teaser: Use the redhat.sso collection sso_realm role to fully configure an authentication
  realm
notes:
- type: text
  contents: |-
    # Single Sign-On configuration

    We deployed a Single Sign-On service on two nodes, in HA configuration. Now we need to configure resources in it that enables an external application to consume authentication of users.

    The `redhat.sso` collection will come handy again as it provides a role specifically for this purpose.

    ![hub-sso-realm.png](../assets/hub-sso-realm.png)
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
difficulty: intermediate
timelimit: 600
---
 💡 Auth realm and EAP subsystem
===
#### Estimated time to complete: *20 minutes*<p>


☑️ Task 1 - Load the repository directory in the editor
===

1. Go to the **editor** tab, clicking on the link in topbar; if the git repository is still open from the previous challenge, proceed to Task 2 below.
2. In the **editor** tab, click on the File menu, then **Load directory**
3. Select the **eap-sso** directory, which is the working copy of the git repository
4. Click **OK** and then confirm in the dialog that open, that you trust the contents


☑️ Task 2 - Create a realm playbook
===

1. In the editor page, make sure you are in the EXPLORER view, by pressing **Ctrl-Shift-E** or clicking on the first button on the left button bar.
2. Click **File** menu, then **New File..**
3. In the dialog that opens, type **sso_realm.yml**, **Enter**
4. Make sure the path is **/home/rhel/eap-sso/sso_realm.yml** and click **OK**
5. You should have now an empty file editor tag, named **sso_realm.yml**
6. Paste the following contents:
```yaml
---
- name: Playbook for rhsso Hosts
  hosts: sso
  become: true
  tasks:
    - name: "Run the realm configuration"
      ansible.builtin.include_role:
        name: redhat.sso.sso_realm
        apply:
          delegate_to: "{{ ansible_play_hosts | first }}"
          run_once: true
      vars:
        sso_admin_password: "{{ admin_pass }}"
        sso_realm: addressbook
        sso_clients: "{{ realm_clients }}"
```
   The playbook above invokes the  **sso_realm** role of the **redhat.sso** collection. We pass the `sso_admin_password` parameter, like in the previous Challenge. We also pass the name for the realm in the `sso_realm` parameters, and the configuration for it which will be read from the `realm_clients` variable which we will define in group_vars.

7. Type **Ctrl-S** to save, or use the **File**/**Save** menu
8. Locate the **deploy.yml** file, and click to open it in a new editor tab
9. To add the newly create playbook in the main playbook, on line 6 (after sso.yml and before eap.yml), type:
```yaml
- import_playbook: sso_realm.yml
```

10. Type **Ctrl-S** to save, or use the **File**/**Save** menu

Ok, we now have the playbooks in; let's configure the collection in the next challenge.


☑️ Task 3 - Configure the SSO realm client
===

The client for the SSO realm is the addressbook web application; let's configure it.

1. In the editor page, make sure you are in the EXPLORER view, by pressing **Ctrl-Shift-E** or clicking on the first button on the left button bar.
2. In the EXPLORER panel, expand the **inventory/group_vars** directory, and open the **sso.yml**
3. You will be presented with a new editor tab contining the existing **sso** group variables; append the following at the end of the file:
```yaml
realm_clients:
  - name: addressbook
    client_id: addressbook
    roles:
      - admin_role
      - user_role
    realm: addressbook
    public_client: true
    web_origins: '+'
    redirect_uris: '*'
    users:
      - username: administrator
        email: ansible-middleware-core@redhat.com
        firstName: Admin
        lastName: Admin
        password: password
        client_roles:
          - client: addressbook
            role: admin_role
            realm: addressbook
          - client: addressbook
            role: user_role
            realm: addressbook
      - username: user
        email: your.email@address.com
        firstName: myFirstName
        lastName: mySurname
        password: password
        client_roles:
          - client: addressbook
            role: user_role
            realm: addressbook
```

   The above configuration will create an *addressbook* client in the *addressbook* realm, with two roles: `admin_role` and `user_role`. Then it will create two users: `administrator` with both roles, and `user`, beloging to the `user_role` only. The **addressbook** web application version 1.1.0, which we deployed, will authorize users that belong to the `user_role` role.

4. Find the `password`s for the users, and update with a password of your choice
5. Update the `firstName` and `lastName` of the `user` user with your own
6. Type **Ctrl-S** to save, or use the **File**/**Save** menu


☑️ Task 4 - Configure the EAP keycloak subsystem
===

Now that we have Single Sign-On deployed and the addressbook realm configured, we will need to update the JBoss EAP configuration to integrate on it, via its `keycloak` subsystem. To do so, perform the following steps:

1. In the editor page, make sure you are in the EXPLORER view, by pressing **Ctrl-Shift-E** or clicking on the first button on the left button bar.
2. In the EXPLORER panel, expand the **templates** directory, and open the **eap_ymlconfig.yml.j2** file.
3. Append the following at the end of the file:
```yaml
    keycloak:
      secure-deployment:
        addressbook.war:
          realm: addressbook
          resource: addressbook
          auth-server-url: {{ sso_frontend_url }}/
          ssl-required: external
          disable-trust-manager: true
          use-resource-role-mappings: true
          verify-token-audience: true
          public-client: true
```

**IMPORTANT**: mind the indent! The `keycloak` key should have the same indent of the `datasources` key on line 21.

4.Type **Ctrl-S** to save, or use the **File**/**Save** menu


☑️ Task 5 - Commit changes
===

1. Switch to the **Source Control** git dialog (third icon on the left column, should have a blue notification).
2. Fill the dialog text called **Message** with `Add SSO REALM playbook`
3. Click on the blue **Commit** button to apply the changes. You will notice that while the editor suggests to synchronize changes (ie. a git push) to the remote repository, however this operation is not necessary for our workshop.



✅ Next Challenge
===
Press the `Check` button below to go to the next challenge once you’ve completed the task.

🐛 Encountered an issue?
====

If you have encountered an issue or have noticed something not quite right, please [open an issue](https://github.com/ansible-middleware/instruqt/issues/new?labels=a4mw-eap-sso&title=Issue+with+Deploy+Red+Hat+Single+Sign-On+with+Ansible+for+Middleware+collections+slug+ID:+a4mw-eap-sso-auth-realm&assignees=guidograzioli).

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
