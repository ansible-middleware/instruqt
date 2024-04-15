---
slug: a4mw-eap-sso-redeploy
id: r4ul612idzfw
type: challenge
title: Update the web application deployed in EAP
teaser: Our developers have built a new version of the webapp, which requires authentication
notes:
- type: text
  contents: |-
    # Rinse and repeat

    It's time to make our first edit to the scm repository holding our environment configuration. The development team has sent our way
    version 1.1.0 of the addressbook web applcation, which now requires an external authentication method, to be provided by connecting JBoss EAP
    with a service called Red Hat Single Sign-On.

    Let's start by updating the Ansible configuration to download and deploy this new version inside EAP, and see how it goes.
- type: text
  contents: "# Quick recap\n\nTo recap where we are, after our first deployment:\n*
    We have the host `jbcs-eap` running JBCS as a reverse proxy\n* The same `jbcs-eap`
    host also runs JBoss EAP, and we have the web application *addressbook* version
    1.0.0 deployed in it. It looks like:\n\n![addressbook.png](../assets/addressbook.png)\n\nRemember
    it, because we are about to break it \U0001F601"
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
- title: addressbook
  type: service
  hostname: jbcs-eap
  path: /addressbook/
  port: 443
difficulty: basic
timelimit: 600
---
 💡 Redeploy
===
#### Estimated time to complete: *10 minutes*<p>


☑️ Task 1 - Load the repository directory in the editor
===

1. Go to the **editor** tab, clicking on the link in topbar; if the git repository is still open from the previous challenge, proceed to Task 2 below.
2. In the **editor** tab, click on the File menu, then **Load directory**
3. Select the **eap-sso** directory, which is the working copy of the git repository
4. Click **OK** and then confirm in the dialog that open, that you trust the contents


☑️ Task 2 - Update the version of the web application
===

1. In the **editor** tab, find and open the **inventory/group_vars/eap.yml** file
2. Update the web application download URL, replacing
```yaml,nocopy
app_url: https://github.com/guidograzioli/keycloak/raw/instruqt/addressbook-1.0.0.war
```

with:
```yaml
app_url: https://github.com/guidograzioli/keycloak/raw/instruqt/addressbook-1.1.0.war
```

3. Save with `Ctrl-s`
4. Switch to the **Source Control** git dialog (third icon on the left column, should have a blue notification)
5. If the Source Control panel does not report changes, make sure it does by clicking on the **refresh** button
6. Fill the dialog text called **Message** with `Update web application to 1.1.0`
7. Click on the blue **Commit** button to apply the changes. You will notice that while the editor suggests to synchronize changes (ie. a git push) to the remote repository, however this operation is not necessary for our workshop.


☑️ Task 3 - Locate and run the deploy Template
===

1. Switch to the **Automation controller** tab
2. On the side navigation bar, under the **Resources** section, click on **Templates**
3. Click on the **sso-eap-deploy** template
4. On the page that opens, click the **Launch** button
5. The launch dialog opens the **Survey**, asking for credentials (defaults are already set), click **Next**
6. Click **Launch**; you will be redirected the executing job output page.


☑️ Task 4 - Validate deployment
===

1. Follow the job execution output up to the end
2. Note that all tasks should be ok (green) or skip (cyan), except the very last that perform the deployment of the newly downloaded web application.
3. Also notice how a mostly unchanged execution run much faster than the initial deployment, as it is only verifying the configuration during most the
   execution. Playbooks and collections that only report changes when actual change operations are commited to the target hosts are called
   **idempotent**; while it is not always possible to implement idempotency in collections, relying on those who are, represents a huge advantage when
   handling configuration drift.

   That is, because an idempotent collection will only report an _ok/not changed_ outcome when the expected configuration is the one which is defined in the scm repository; and reversely, will report a _changed_ state when commits were applied to the scm repository, thus, raising the trust on the _declared configuration in the scm repository being the **single source of truth**_ for the configuration of a live system.

   Any changes that wouldn't follow an scm commit, would have to be considered drift: important to account for, and with the added benefit that Ansible will _fix_ the unexpected state pro-actively, applying the expected configuration while reporting the change.
4. When the execution ends successfully, click on the **addressbook** tab and hit the ↻ refresh button. Remember we opened the same web application during Challenge 2, just after we executed our first deployment.
5. You should get an error, likely **Forbidden**, because the web application deployment failed (in turn, because it requires an authentication service that is not yet deployed: we will configure the deployment of it in the next challenges). If it does not, give it a few more second, and hit the refresh button again
6. To verify the new version was deployed, switch to the **Terminal** tab in the top menu, and type or paste the command:
```ssh root@jbcs-eap grep WFLYSRV0016 /opt/jboss_eap/jboss-eap-7.4/standalone/log/server.log```

   to check the JBoss EAP logfile. It should show a line indicating, as expected, `WFLYSRV0016: Replaced deployment ..` confirming the new web application version has been deployed.


✅ Next Challenge
===
Press the `Check` button below to go to the next challenge once you’ve completed the task.

🐛 Encountered an issue?
====

If you have encountered an issue or have noticed something not quite right, please [open an issue](https://github.com/ansible-middleware/instruqt/issues/new?labels=a4mw-eap-sso&title=Issue+with+Deploy+Red+Hat+Single+Sign-On+with+Ansible+for+Middleware+collections+slug+ID:+a4mw-eap-sso-redeploy&assignees=guidograzioli).

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
