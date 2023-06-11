---
slug: a4mw-eap-sso-redeploy
id: r4ul612idzfw
type: challenge
title: Update the web application deployed in EAP
teaser: Our developers have built a new version of the webapp, which requires authentication
notes:
- type: text
  contents: |-
    # Redeploy



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

1. Go to the **editor** tab; if the git repository is still open, process to Task 2 below.
2. In the **editor** tab, click on the File menu, then **Load directory**
3. Select the **eap-sso** directory, which is the working copy of the git repository
4. Click **OK** and then confirm in the dialog that open, that you trust the contents


☑️ Task 2 - Update the version of the web application
===

1. In the **editor** tab, find and open the **inventory/group_vars/eap.yml** file
2. Update the web application download URL, replacing `app_url: https://github.com/guidograzioli/keycloak/raw/instruqt/addressbook-1.0.0.war` with `app_url: https://github.com/guidograzioli/keycloak/raw/instruqt/addressbook-1.1.0.war`, and save with `Ctrl-s`
3. Switch to the **Source Control** git dialog (third icon on the left column, should have a blue notification)
4. Fill the dialog text called **Message** with `Updating web application download URL`
5. Click on the blue **Commit** button to apply the changes


☑️ Task 3 - Locate and run the deploy Template
===

1. Switch to the **Automation controller** tab
2. On the side navigation bar, under the **Resources** section, click on **Templates**
3. Click on the **sso-eap-deploy** template
4. On the page that opens, click the **Launch** button
5. The launch dialog open, asking for credentials (defaults are already set), click **Next**
6. Click **Launch**; you will be redirected the executing job output page.


☑️ Task 4 - Validate deployment
===

1. Follow the job execution output up to the end
2. Note that all tasks should be ok (green) or skip (cyan), except the very last that perform the deployment of the newly downloaded web application.
3. Also notice how a mostly unchanged execution run much faster than the initial deployment, as it is only verifying the configuration during most the execution.
4. Now click on the **addressbook** tab and hit the ↻ refresh button
5. You should get an error, because the web application deployment failed (in turn, because it requires an authentication service that is not yet deployed: we will configure the deployment of it in the next challenges)


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
